# GRAP
Utility that GReps for gAPs and out of sequence line in log files

## Installing
```
npm install grap -g
```

## Usage
For example, given the logs file in `test/sample.log`:

```
Dec 08 03:00:14.035 DEBUG  Something interesting happened
Dec 08 03:00:14.036 DEBUG  Something interesting happened
Dec 08 03:00:14.037 DEBUG  Something interesting happened
Dec 08 03:00:14.025 DEBUG  Something interesting happened
Dec 08 02:00:14.038 DEBUG  Something interesting happened
Dec 08 03:00:16.035 DEBUG  Something interesting happened
Dec 08 03:00:15.035 DEBUG  Something interesting happened
```

Anything look out of place to you? Probably not. humans are not very good at performing repetitive tasks. Let's run grap to see what it finds:

```
# grap test/sample.log
Dec 08 03:00:14.025 DEBUG  Something interesting happened
Dec 08 02:00:14.038 DEBUG  Something interesting happened
Dec 08 03:00:15.035 DEBUG  Something interesting happened
```

Hmm. It seems that 3 log lines are out of sequence. The first one is a few milliseconds back in time, the second about an hour and the third a fujll second before the previous line.

You can also pipe text to grap and it will work in the same way:

```
# cat test/sample.log | grap
Dec 08 03:00:14.025 DEBUG  Something interesting happened
Dec 08 02:00:14.038 DEBUG  Something interesting happened
Dec 08 03:00:15.035 DEBUG  Something interesting happened
```

## Options

- `--dateOffset` (default 0) Tells grap where the date part of the log line starts 
- `--dateFormat` (default 'MMM DD HH:mm:ss.SSS Z') Tells grap how to parse the date. See http://momentjs.com/docs/#/parsing/string-format 
