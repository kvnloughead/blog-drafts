I've got a tip to share. Recently I've been working on screencasts for the deployment section of this sprint, so I've created a bunch of VM's. And whenever I create a new one, there is this terrible bell sound that occurs when do something the terminal doesn't like. Like hit the left arrow key when there is no text written at the prompt. I hate these bells, and have them disabled locally. Here is how you can disable them too.

Open .bashrc with $ nano ~/.bashrc
Scroll to bottom and add the line bind 'set bell-style none'
Run source ~/.bashrc. Without this, the changes won't take effect until your next terminal session.
