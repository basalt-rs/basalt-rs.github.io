# Hashing

There are reasons you may want to compute the hash of your configuration. There
are some nuances to this calculation.

Firstly, it is not based on the file itself. It is based a subset of on the
parsed configuration. This means that whitespace changes and a handful of
properties will have no impact on the hash.
