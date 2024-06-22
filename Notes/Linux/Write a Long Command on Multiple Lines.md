To write one command in more than one line, use a backslash character (\), which is referred to as
the escape character. The backslash character ignores the meaning of the following character.
`[user@host ~]$ head -n 3 \`
`/usr/share/dict/words \`
`/usr/share/dict/linux.words`
`==> /usr/share/dict/words <==`
`1080`
`10-point`
`10th`
`==> /usr/share/dict/linux.words <==`
`1080`
`10-point`
`10th`


when you use space make sure to escape it if you wanna use it on bash or terimanl, example :
Anime\\ -\\ Episode\\ 1


