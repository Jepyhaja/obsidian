Käytetyt ohjeet:
https://www.youtube.com/watch?v=H6ipjzaN2WY
https://www.xypnox.com/blag/posts/moving-notes-to-github/


```bash
#!/bin/bash

gstatus=`git status --porcelain`

if [ ${#gstatus} -ne 0 ]
then

    git add --all
    #sleep 10
    git commit -m "$gstatus"
		#sleep 10
		git pull --rebase
		#sleep 10
    git push

fi
```
