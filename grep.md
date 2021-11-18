---
title: 'Grepping a `man` page'
excerpt: ''
coverImage: ''
date: '2021-11-17'
author:
  name: Kevin Loughead
ogImage:
  url: ''
---

Ever run into a command line in the wild and wondered "huh, I wonder what those 
flags do?" Perhaps you're trying to install Node on Ubuntu, and find this command:

```plain-text
$ curl -sL https://deb.nodesource.com/setup_16.x -o nodesource_setup.sh
```

You might break out the `man` page, with

```plain-text
$ man curl 
```

and then search through it for the flag. Maybe you remember that in a `man` page
you can search for patterns using the `/` key. Personally, I remember that every
time I look it up.

Well, I'm going to tell you about another option. One that... actually isn't any
easier to remember I guess. But I find it a bit more pleasant, and it makes you
feel like a wizard. All you gotta do is pipe the `man` page into `grep`. Try it
like this:

```plain-text
$ man curl | grep -- -s,
```

The result should be pretty effective — we learn that `-s` stands for 'silent'. 
Of course, the results are a bit jumbled, so if you need more details, refer to 
the actual `man` page. But for a quick grok this sometimes does the trick.

There are a few things to point out in the command we used. First, the pipe 
character , `|`. This character takes the output of the program on its left
and "pipes" it into the program on its left. So, we're feeding the text of 
the `man` page to grep. Also, the `-s,` is what we are searching for. I'm added
the `,` to filter out the results a bit. Since `man` pages tend to follow a 
standard format, you should be able to use that in general to search for flags.

But then what's the `--` in between `grep` and `-s,`? We will actually have to
look to the `man` page for bash for this one.

```plain-text
$ man bash | grep -- ' -- '
A -- signals the end of options and disables further option processing...
```

So basically, the `--` is signalling to `grep` that whatever follows it is not
a flag. If you don't use it, then `grep` will think that `-s` is a flag. Now,
you might be thinking, "but couldn't we just quote the darn thing?" Well, the
answer is yes, but it's tricky. Because quoting in bash is tricky. Alright, 
let's try some stuff. If you try each of the following:

```plain-text
$ man curl | grep '-s,'
$ man curl | grep "-s,"
$ man curl | grep `-s,`
```

you'll see that they each fail in their own way. I'm not entirely sure why, but 
I'm sure there's a very good and confusing reason. Now try these:

```plain-text
$ man curl | grep ' -- '
$ man curl | grep " -- "
```

They work! But what about these:

```plain-text
$ man curl | grep '--,'
$ man curl | grep "--,"
```

... they don't work. And in case you are wondering, this

```plain-text
$ man curl | grep ' -s, '
```

is a valid command. The only problem is, we don't want to search for those space!
So what is going on here? I don't even know. Maybe I'll do a part 2 where I bang
my head against the wall of Bash quoting. Until then, I'll stick with using the 
`--` command. 