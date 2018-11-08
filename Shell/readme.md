# Shell Notes

**Sudo !!**
- Add sudo to the previous command, without having to write the previous command. 
Example: 
```bash 
$ apt-get install nvm
$ sudo !!
```
---

## Text Shortcuts
- Move to the start of a sentence: `ctrl+a`
- Move to the end of a sentence: `ctrl+e`
- To cut word by word: `ctrl+w`
- To cut to the end of the sentence, from the beginning of the sentence: `ctrl+k`
- To cut to the beginning of the sentence, from the end of the sentence: `ctrl+u`
- To paste all of the things mentioned above: `ctrl+y`
- To paste the last word of the previous command: `alt+.`
- While writing something, if we want to open the things typed in text editor, then: `ctrl+x+e`
- Move forward one word: `alt+f`
- Move backward one word: `alt+b`

---

**Terminate the shell session**: `ctrl+d`

---

**Clear the terminal**: `ctrl+l`

---

## View Shell history: 
- `history`
- To search commands through history: `ctrl+r`
- Use `ctrl+r` again to shuffle through the options displayed. 
- Use `ctrl+g` to get back to where you left off before history searching

---

**List view of all the files:** `ll`

---

**Find Default Gateway:** `ip r`

---

**Basic info about PC:** `hostnamectl`

---

**In-Depth info about PC:** `inxi -Fxz `

---

**Launch apps from Terminal in the background:** 

Use the `&` keyword at the end of the appname. 
Example: 

`vlc &`

--- 

**Print environment variables:**  `printenv`

---

## ZSH Configuration: 

- **Create Alias with parameters**
Usually if you want to insert parameters in zsh you have to create a function. The function name is the alias we want to create. The index off the parameters are denoted by using `$` symbol. Where `$1` resembles the first variable inpput, `$2` resembles the second variable input and so on.

**Example**
acs(){
apt-cache search $1 | grep $1
}

- The above command places the variable in both the places when you type it the first time.
---




 
