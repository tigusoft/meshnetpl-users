Using crypto
============

Your goals - below we describe how to do them:

[ ] have good GPG config
[ ] generate PGP/GPG key
[ ] export publickey of your PGP
[ ] check git PGP signatures done by others
[ ] get and trust the keys of others

[ ] set git to sign in PGP your work too!

[ ] generate ssh key
[ ] now in git publish the ssh public key,
[ ] ...of course GPG sign the git commit

[ ] get admins on chat IRC server icann.irc.meshnet.pl / h.irc.meshnet.pl (port 9999 for SSL),
to merge your changes. This must be done very quickly otherwise the commit signatures will not
work (you would have to re-do them after rebase). Or email: meshnetpolska at gmail.com; 
Or github poll request.

How to do all above:

PGP keys - GPG configuration
----------------------------

Install program gpg, run it at least once like: `gpg -K`

Then copy this *gpg.conf* into your *~/.gnupg/gpg.conf* (or other place for your gpg configuration)
before (or after) making the copy, inspect the file to make sure it is fine, it should just
force some more secure defaults stronger encryption and so on.

If not sure check online or comment out parts (lines) of it with hash character.

PGP key - new key
-----------------

Run program and give following options:
`gpg --gen-key`
1
4096
5y # or other number of years, remeber to recreate/update the key by that date
then your name and email (of course can be what ever you want)
and the comment field, nothing, or maybe e.g. "laptop, medium secure" or "offline work pc, secure" or "travel table, insecure"

When the program is done (it can take few minutes) then see the keys: `gpg -K`

Dump the new key:
`gpg --export --armor 1234ABCD > yourname.pub`
where 1234ABCD is your key number.

Move the .pub file where needed here.

PGP key - configure for git
---------------------------

In the working directory of this git project (e.g. here) do,
of course replacing the data with your data:
```
git config --local  user.email "user@you.example"
git config --local  user.name  "Your Name"
git config --local  user.signingkey "FAFABABA1234ABCD"
```

PGP key in git
--------------

Add option -S to commits, like `git commit -S ........`
and option -s to tags like `git tag -s v0.5`

Then your commits, and your tags, will be PGP signed.
Check it: 
`git log --show-signature`
if some key is missing there, then import it like `gpg --import user/his.pgp.key.pubkey` taking files from here
or from other trusted source.

Now it will say it is signed, but that signing key is not trusted. To trust the key, do:
gpg --edit-key AAAABBBB  (where AAAABBBB is the key of other user, you see them listed in `gpg -k`)
ther do interactive command:
`fpr`
and very carefully, best in-person, check the key (or using other very secure channel) with the key owner, then:
`trust`
and select trust level 5 or 4 or other depending on how well the key is verified. Then quit
`quit`

Now again show the git log, it should say the signature is fully valid.

Same goes for checking tags, check them as: `git tag -v v0.5`.

SSH key
-------

Generate with:
`ssh-keygen -t rsa -b 16384`
Yes, 16384, so if it would happen that QC devices are not-linear in cost of building depending on the qbit size,
then it could be much better then 4096, even if the key-breaking time would be sub-exp, e.g. close to log.
Though 4096 keys are acceptable too by us for now too.

If you had other key, then save new one in file named e.g. `id_rsanew`.

Publish the *public* key, named as .pub, e.g.:
`~/.ssh/id_rsa.pub` (double check if it's .pub :)
copy it here in reasonable place/name.




