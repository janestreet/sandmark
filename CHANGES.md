### v1.2.0 2020-07-07 Paris (France)

- add LZO support (@dinosaure, @cfcs, @XVilka, #82)
- update binaries (@dinosaure, @XVilka, #89)
- fix an exception leak (@dinosaure, @b1gtang, #88)
- update README.md (@dinosaure, @XVilka, #87)
- fix a mis-use of `Zl` API (@dinosaure, #85)
- add `dune` as a dependency of `rfc1951` (@kit-ty-kate)
- real non-blocking state with `Zl` (@dinosaure, #84)

### v1.1.0 2019-03-10 Paris (France)

- add GZip support (@dinosaure, @copy, @hcarty, #79)
- **breaking changes**, `Higher` returns a `result` value instead to raise an exception (@dinosaure, @copy, #80)
- protect Zlib decoder on multiple _no-op_ calls of `decode`
- test when we generate an empty zlib flow
- fix a bug on the DEFLATE layer when we must flush bits to avoid integer overflow
- really use the internal continuation of the Zlib state
- delete `fmt` depedency
- update fuzzer
- fix default level on `Zl.Higher`

### v1.0.0 2019-08-30 Paris (France)

** breaking changes **

`decompress.1.0.0` is 3 times faster about decompression than before. A huge
[amount of work was done](https://tarides.com/blog/2019-08-26-decompress-the-new-decompress-api.html) to improve performance and coverage.

The main reason to update the API is to fix a bad design decision regarding split
compression and encoding. User is able to implement a new compression algorithm
and use it.

Release comes with regressions:
- `decompress` only supports `Bigarray` now, not `Bytes`
- GZIP layer does not exist anymore
- state of RFC1951 encoder/decoder is not referentially transparent anymore

Of course, v1.0.0 comes with fixes and improvements:
- `decompress` is able to compress/uncompress [Calgary corpus](https://en.wikipedia.org/wiki/Calgary_corpus)
- tests are improved and they include all coverage tests from `zlib`
- compression algorithm has a fuzzer
- encoder has a fuzzer
- performance about decoder is 3 times better than `decompress.v0.9.0` and 3
  times slower than `zlib`

`decompress` is split into 2 main modules:
- `dd` which implements RFC1951
- `zz` which implements ZLIB

API of them are pretty-close to what `decompress.v0.9.0` does with some
advantages on `dd`:
- User can use their own compression algorithm instead of `Dd.L`
- encoder exposes more granular control over what it emits (which block, when, where)
- Huffman tree generation is out of `dd`

As a response to #25, `dd` provides a _higher_ level API resembling `camlzip`.

### v0.9.0 2019-07-10 Paris (France)

* Add support of 4.07 and 4.08 in Travis (@XVilka, @dinosaure, #70, #71)
* Use `mmap` (@XVilka, @dinosaure, @hannesm, #68, #69, #71)
* Update documentation (@yurug, @dinosaure, #65, #66)
* Micro-optimization about specialization (@dinosaure, #64)
* Re-organize internals of `decompress` (@dinosaure, #63) 
* GZIP support (@clecat, review by @dinosaure, @cfcs, @hannesm, #60)
 - fix #58 (@dinosaure)

### v0.8.1 2018-10-16 Paris (France)

* _Dunify_ project (@dinosaure)
* *breaking-change* Unbox `Bytes.t` and `Bigstring.t` as I/O buffer (@dinosaure)
* Add foreign tests vectors (@cfcs, @dinosaure)
* Catch invalid distance (@XVilka, @dinosaure)
* Better check on dictionaries (@XVilka, @dinosaure)
* *breaking-change* Add [wbits] argument to check Window size on RFC1951 (@XVilka, @dinosaure)

### v0.8 2018-07-09 Paris (France)

* Implementation of RFC1951 (task from @cfcs)
* *breaking change* New interface of decompress

  We wrap API in `Zlib_{inflate/deflate}` and add `RFC1951_{inflate/deflate}`.
  
* Move to `jbuilder`/`dune` (task from @samoht)
* Better check on `zlib` header
* Fixed infinite loop (task fron @cfcs)

  See 2e3af68, `decompress` has an infinite loop when the inflated dictionary
  does not provide any bindings (and length of opcode is <= 0). In this case,
  `decompress` expects an empty input and provide an empty output in any case.
  
* Use re.1.7.2 on tests
* Use camlzip.1.07 on tests

### v0.7 2017-10-18 Paris (France)

* Fixed Inflate.write function
* Fixed internal state to stick in a internal final state
* Fixed compilation with js_of_ocaml (use trampoline function to avoid
  stack-overflow)
* Fixed clash of name about state variable in the Inflate module
* Add afl program
* Export Adler-32 modules
* Add -i and -o option in the dpipe binary to inform the size of the
  internal chunk
* Change the value of -mode in the dpipe binary

### v0.6 2017-05-11 Cao Lãnh (Vietnam)

- Fixed bug #29
- Produce far pattern (Lz77 compression)
- Optimize memory consumption of the Inflate module
- Move repository from oklm-wsh to mirage
- Learn topkg release

### v0.5 2017-02-17 Essaouira (Maroc)

- Stabilize the interface (@dbuenzli's interface)
- Merge optimization from @yallop
- Add `sync_flush`, `partial_flush`, `full_flush` (experimental)
- Move the build system to `topkg`
