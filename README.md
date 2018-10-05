# Common password topology detection

The aim of this library is to provide developers with libraries for multiple
languages that will detect the use of a common password topology as determined
by analysis done on leaked password databases.


## Topology example

Breakdown:
  - `U`: Uppercase
  - `l`: lowercase
  - `d`: digit
  - `p`: punctuation (this lib determins `p` to be anything not matching pervious criteria)

Given this password:

  Abcd 01 !

The resulting topology would be:

  Ulllpddpp


## leak-analysis/
This folder contains json files with the results of analysis done on ~1.5b
passwords from leaked databases.

Example structure:
```json
[
  {
    "count": 369184116,
    "regexp": "[l]+p",
    "topology": "llllllllp",
    "largest": 51
  }
]
```

Field breakdown:
  - count: number of occurances matched the `regexp` rule
  - regexp: regular expression that matches the topology
  - topology: an example of the topology the `regexp` should match
  - largest: the largest password that `regexp` matched

File description:
  - `owasp-ex-len-topologies.json`: Passwords that match the criteria of `U` + `l` + `d` + `p` without the criteria of length of 10+chrs
  - `owasp-topologies.json`: Passwords that match the criteria of `U` + `l` + `d` + `p` with the criteria of length of 10+chrs
  - `top-100-*.json`: Top 100 (count sorted) only
  - `topologies-count-gt-1000`: All topologies with a `count` greater than 1000
  - `topologies.json`: All topologies found