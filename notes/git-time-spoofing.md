## How to spoof git commit times

Some users may wish to conceal the time that they are committing code. To do so, simply add the following to your ~/.bashrc or ~/.zshrc:

```bash
RAW_DATE=$(date -uIminutes)
export GIT_AUTHOR_DATE=${RAW_DATE::-11}00:00:00
export GIT_COMMITTER_DATE=${RAW_DATE::-11}00:00:00
```

To [anyone inspecting your commits](https://chainbulletin.com/satoshi-nakamoto-lived-in-london-while-working-on-bitcoin-heres-how-we-know), it will look like you are always committing at 00:00:00 UTC time.
