# GitHub CLI

## Device Flow Login

When asked to "gh login", always use nohup + background + read log:

```bash
nohup gh auth login --hostname github.com --git-protocol https -p https -w > /tmp/gh-login.log 2>&1 &
sleep 3 && cat /tmp/gh-login.log
```

Never use `timeout`. The shell tool is synchronous — it blocks until the command finishes, so stdout won't be visible until then. `nohup` runs it in the background, `sleep 3 && cat` grabs the code immediately.
