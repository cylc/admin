# `cylc flow` CLI proposal

## Purpose
Specify how the Cylc8 command to replace `rose-suite-run` will work.

## References
[cylc-flow #1030](https://github.com/cylc/cylc-flow/issues/1030).

## Discussion of possible names for new command

Possibilities include:

| Name | For | Against |
| --- | --- | --- |
|`cylc run`||Already in use for another command|
|`cylc suite-run`|similar to `rose suite-run` -familiar|similar to `rose suite-run` -confusing<br>Quite long|
|`cylc`|Short<br>Hints at the core-ness of this command to Cylc|Already in use|
|`cylc flow`|Consistent naming<br>Like nothing currently in use  ||
|`cylc go`|Short|Confusable with `rosie go`|
|`cylc execute`/`exec`||Long<br>Too generic|
||||

For the remainder of this document this command will be referred to
as `cylc flow`.


## Discussion of functionality available

The following functionality may be necessary or desirable:

* Restart a suite from last checkpoint (`--restart`, `--continue`
  `--resume`).
* Restart a suite at a given checkpoint (`--restart-from`,
  `--continue-at`,  `--continue-from`).
* Restart a suite from an arbitary point (warm start, `--warm-start`,
  `--restart-from`, `--continue-from`).
* Cool start - start a suite from the beginning without cleaning install or
  rebuilding. (`--restart-at BEGINNING`, `--dc-al-coda`?)
* Cold start a suite - start a suite from the beginning carrying out build
  tasks (`--rebuild`) but not necessarily cleaning any logs.
* Clean start a suite - start a suite having cleaned out any data generated
  (`--clean`) but not carrying out a full rebuild.
* Both of the above at once?
* Increment start a suite - start a new, clean, experimental iteration with
  different data location but perhaps sharing some compiled material from
  cold start (`--increment`, `--increment PATTERN`)? If you had
  `cylc flow --increment --name MyExperiment` you'd get suites `MyExperiment_0`,
  `MyExperiment_1`... and so on.

n.b. "Restart" has traditionally meant "continue from last checkpoint" rather
than "restart from the beginning" and to avoid confusion this meaning should
be continued. Since it isn't totally obvious this definition should probably be
noted as a warning box in the documentation.

Another way of looking at this would be :
<table>
<tr>
<td colspan=2 rowspan=2></td><td colspan=2>Clean the installed files</td>
</tr><tr>
<td>yes</td><td>no</tr>
</tr><tr>
<td rowspan=2>Start suite from the beginning</td><td>yes</td><td>clean-run or increment</td><td>cylc flow</td>
</tr><tr>
<td>no</td><td>Is this desirable? <br> might you want a clean "warm start"<br> to remove corrupted files?</td><td>"restart" or "continue" from checkpoint<br>"Warm start" from arbitary point</tr>
</table>
