### how to encrypt and decrypt a file

I find three methods to encrypt/decrypt a single file. Those ways use
different utilities respectively, which are vim, gpg and openssl. I prefer
to use vim, because vim is really convenient. I will cover two of them.

#### vim

For example, I have a file named `info` including many important information in
my home directory, so I don't want others to read it. To encrypt this file,
we could do this:

<div class="code"><pre>
<tt>billie@piggy:~$ vim -x info</tt>
</pre></div>

After run this command, you will get prompt at the bottom of your screen.

<div class="code"><pre>
<tt> Enter encryption key: 
Enter same key again: </tt>
</pre></div>

Enter your passward according to the prompt, then the job is done. If you want
to see the content of this file next time, you need to enter passward,
otherwise you will see bullshit.

In addition, you may change your password. To do this, execute the following
command in your terminal.

<div class="code"><pre>
<tt>billie@piggy:~$ vim +X info</tt>
</pre></div>

The command above will prompt some messages.

<div class="code"><pre>
<tt>"info" [crypted] 1L, 3C
Enter encryption key: 
Enter same key again: </tt>
</pre></div>

Note once you encrypted your file, you will not get its cleartext back unless you
remember the encryption key.

#### gpg
gpg is another tool to encrypt files. Check gpg man page for more details. You
can use it like this:

<div class="code"><pre>
<tt>billie@piggy:~$ gpg -c info
Enter passphrase: 
Repeat passphrase:</tt>
</pre></div>

gpg will create a new file called info.pgp, and the info file still exist,
so you need to remove the original file manually.  

<div class="code"><pre>
<tt>billie@piggy:~$ gpg -d info.pgp -o info
Enter passphrase: </tt>
</pre></div>

The "-o" option redirect the output to the file info.
