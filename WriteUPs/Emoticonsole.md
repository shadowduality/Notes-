
Two files : __program.emo__ & a __.pym file__

Ran file : 
`
file <name_of_file>
`

<img src="https://imgur.com/euGhByd.png"></img>

<img src="https://i.imgur.com/AmNPDF6.png"></img>

I also tried several other tools. I kept playing around and thinking of different things to try.  I found that this challenge was pretty difficult, but I'm not used to reverse engineering.  While it was challenging, I found it enjoyable.  

<a href="https://www.tutorialspoint.com/What-are-pyc-files-in-Python">__What is .pyc ?__</a>


__.pyc is compiled bytecode__

How to extract?
I tried a few tools before I found: <a href="https://github.com/zrax/pycdc.git
">__pycdc__</a>

`git clone https://github.com/zrax/pycdc.git`


It required __cmake__

`cd pycdc
cmake CMakeLists.txt
make`

then

<img src="https://i.imgur.com/9kDRsaT.png"></img>

`pycdc <filename> -o <fileoutputname>`
--o is for output--

`cat newfile.py` to view created filed

I like using Visual Studio code. To open the file in Visual Studio: 

<img src="https://imgur.com/7K3JDmf.png"></img>

`code ./name_of_newfile.py`

Ok, so now that's it opened I took quite a bit of time playing around with print.  

tried to run file 
`python3 ./name_of_newfile.py` and was met with an error. 

I also tried <a href="https://github.com/serfend/pydumpck">__pydumpck__</a> and <a href="https://github.com/rocky/python-uncompyle6"> __uncompyle6__ </a> without much success. 

Eventually I used <a href="https://pylingual.io/">Pylingual</a>

It took me a while to familiarize myself with the code, and the primary way I did that was by printing variables. Then printing anything I could, running the program, and printing in different places. I got some interesting output: 

`W[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179, 224, 250, 179, 231, 242, 251]`
`h[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179, 224, 250, 179, 231, 242]`
`a[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179, 224, 250, 179, 231]`
`t[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179, 224, 250, 179]`
 `[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179, 224, 250]`
`i[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179, 224]`
`s[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231, 179]`
 `[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251, 231]`
`t[153, 153, 179, 172, 244, 242, 255, 245, 179, 246, 251]`
`h[153, 153, 179, 172, 244, 242, 255, 245, 179, 246]`
`e[153, 153, 179, 172, 244, 242, 255, 245, 179]`
 `[153, 153, 179, 172, 244, 242, 255, 245]`
`f[153, 153, 179, 172, 244, 242, 255]`
`l[153, 153, 179, 172, 244, 242]`
`a[153, 153, 179, 172, 244]`
`g[153, 153, 179, 172]`
`?[153, 153, 179]`
 `[153, 153]`

`[153]`

`[]`

I opened up the emoji file, and I saw this: 
<img src="https://i.imgur.com/rYjU0Eu.png"></img>


I continued to play with the code, and then I noticed that the emojis corresponded to different functions.

        self.EMO = {'🌞': self.emo_func_start, '📥': self.emo_func_input_byte, '🔼': self.emo_func_push_byte, '⊕': self.emo_func_xor_byte, '❔': self.emo_func_jump_if, '🟰': self.emo_func_compare, '🔄': self.emo_func_jump_back, '🔁': self.emo_func_jump_forward, '➖': self.emo_func_subtract, '➕': self.emo_func_add, '🔊': self.emo_func_output_byte, '🌛': self.emo_func_exit}

🌞  
   `self.EMO = {'🌞': self.emo_func_start,`

`def emo_func_start(self, I):`
        `return`
    So, this is the start of the program

🔼
`'🔼': self.emo_func_push_byte`

`def emo_func_push_byte(self, I):`
        `X = int(''.join([self.NUMS[I[i]] for i in range(1, 4)]))`
        `self.STACK.append(X)`
    pushes to the stack

`'⊕': self.emo_func_xor_byte,`

 `def emo_func_xor_byte(self, I):`
        `if len(self.STACK) > 1:`
            `V1 = self.STACK.pop()`
            `V2 = self.STACK.pop()`
            `self.STACK.append(V1 ^ V2)`

If stack is greater than 1, pops off two items from the stack and XORs them (^)

So, I was able to see in the emoji portion of the program that numbers were being added to the stack, then the XOR would be taken and that value recorded 

ex: 🔼⓵⓽⓺🔼⓵⓸⓻⊕🔊
I noticed that these numbers were in decimal format. I used a XOR calculator, and then I also noticed that the values corresponded to ASCII characters.
196 XOR 147 = 87 = W

This is what spells out `What is the flag?` 
When the program is initially run.
To run the program you use the format `./file.py progam.emo`
Which outputs :  What is the flag? 
<img src="https://i.imgur.com/LOIPf0g.png"></img>


Like i mentioned before I added print statements to various places in the program to get a better idea of what was happening. In retrospect I took too much time here, but I'll admit it was fun.  

Next, I turned my attention to the program.emo.

I had figured out that the __87 104 97 116 32 105 115 32 116 104 101 32 102 108 97 103 63 32 10 
10__values corresponded to ASCII -> What is the flag?

Then, I noticed this section in the emo program. I took the XOR values, matched them up to their corresponding ASCII values and found the flag ->

<img src="https://i.imgur.com/feL6pWY.png"></img>

Emotional Damage!  Yes, yes this was.

<img src="https://tenor.com/view/emotional-damage-emotional-damage-meme-funny-gif-24332819.gif"></img>

<H2> Lessons Learned</H2>
CTFs are incredibly humbling but also addictive.  I learned that I need to work on my programming skills (especially Python), that I needed to develop a methodology for each category, and that in the future it would be a good idea to document as I go. 