Charset editor for Pico 8
-------------------------

written by GPI

copy me, I'm free!

Short manual
------------
A simple tool to create fonts for the virtual console pico8.

Left click on the charset to edit this char. Right click will
copy the current char to this position.

Left click on the char will set a dot, right click will delete it.
With the cursor keys you can shift the current char.
"Set Default" will reset the current charater to the default.

"Lo Width" are for chars with a code <= 127, "Hi Width" for code >=128.

With "Copy" and "Paste" you can copy the complete Charset to the clipboard as
a string embeded in [[ ]]. Don't indent the string, it could change the font!
In pico 8 you need the following code to transfer the string to the memory:

	function str2mem(data)
		local t,a,i,c,d,str,m = split(data)
		for a = 1,#t,2 do  
			m,str,i=t[a],t[a+1],1
			while i <= #str do
				c,d= ord(str,i,2)
				i+=c==255 and 2 or 1
				if (c>16) poke(m, c==255 and d or c^^0x80) m+=1
			end
		end
	end
	
	myfont = [[0x5600,
	--some funny chars
	]]
	
	str2mem(myfont)

with "Load" and "Save" you can load/save the current font as ascii-file with
the extension ".lua". It is the same format as the clipboard routines.

About the string format
-----------------------
A Font is too big for a string in "", but enclose it with [[]] has the 
disadvantage that escape-sequenzes are not possible. Also chars lower 16 are not
printable.

Chars lower than code 16 must be encode in a special form. Also some special 
characters like "[]," must be encoded to prevent conflicts.

Because chars lower than code 16 are very common (especially code zero), I first 
flip the high-bit of the char (m = char ^^ 0x80).
If m is now lower 16 or one of the special characters, I store the in the string a
sequenz of "chr(0xff)..chr(m ^^ 0x80)" otherwise a simple "chr(m)".

Infos
-----
Icon made by https://www.freepik.com from https://www.flaticon.com/

