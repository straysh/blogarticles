{
    "id": 12,
    "user_id": 1,
    "category_id": 5,
    "author": "straysh",
    "title": "HOWTO: prevent 'stdin: is not a tty' errors when using ssh",
    "slug": "HOWTO: prevent 'stdin: is not a tty' errors when using ssh",
    "hits": 75,
    "published_at": "1386637204",
    "created_at": 1386637204,
    "updated_at": 1504723470,
    "deleted_at": null
}
link:<a href="http://www.vpshostingforum.com/howto-prevent-stdin-not-tty-errors-when-using-ssh-t4152.html">http://www.vpshostingforum.com/howto-prevent-stdin-not-tty-errors-when-using-ssh-t4152.html</a>
<p>
When you are connecting to a remote server using ssh (for rsync, or other remote functions), and are receiving 'stdin: is not a tty' error messages in your log files, it is most likely because your remote shell is trying to execute something which needs to run interactively, when you are not in an interactive mode.
</p>
<p>
I was experiencing this problem myself, while re-creating my rsync backup system on my new local server, and after looking all over the place for info - I finally found a solution.
</p>
<p>
Of course, the rsync was still working properly, but having it generate errors was keeping me from sleeping
</p>
<p>
Simply add the following line to the top of your .bashrc file (in the home dir of your user account):
</p>

Code:
<pre class="brush:bash">
[ -z "$PS1" ] && return
</pre>
<p>
This will cause bash to check and see if it is running interactively or not, and if it is not, it will halt processing of the configuration file, preventing the rest of the file from executing code which could possibly generate this error when in non-interactive mode.
</p>
<p>
This must be done for each of your user accounts, but if you also make the change in /etc/skel/.bashrc, the 'fixed' version will be used for all new accounts in the future.
</p>

Note: This is the first time I have done anything with bash configuration files, so feel free to let me know if this method will cause any bad results 