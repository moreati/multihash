## Abstract

This specification defines a mechanism by which hash digests may be encoded,
such that the hash function & (possibly truncated) digest size can be determined.

## Introduction

Multihash is a protocol for differentiating outputs from various
well-established cryptographic hash functions, addressing size + encoding
considerations.

It is useful to write applications that future-proof their use of hashes,
and allow multiple hash functions to coexist.
See https://github.com/jbenet/random-ideas/issues/1 for a longer discussion.

## Conformance

The key words may, must, must not, and should are to be interpreted as
described in [RFC2119].

[RFC2119]: https://tools.ietf.org/html/rfc2119

### Key Concepts and Terminology

This section defines several terms used throughout the document.

The term <dfn>digest<dfn> to the result of executing a cryptographic hash
function on an arbitrary block of data.

The term <dfn>digest size<dfn> ...

<dfn>SHA-1</dfn> is a cryptographic hash function defined by the
NIST in ["FIPS PUB 180-4: Secure Hash Standard (SHS)"][shs].

<dfn>SHA-256</dfn>, <dfn>SHA-384</dfn>, and <dfn>SHA-512</dfn> are part
of the <dfn>SHA-2</dfn> set of cryptographic hash functions defined by the
NIST in ["FIPS PUB 180-4: Secure Hash Standard (SHS)"][shs].

<dfn>SHA3-512<dfn> is part
of the <dfn>SHA-2</dfn> set of cryptographic hash functions defined by the
NIST in ["FIPS PUB 180-4: Secure Hash Standard (SHS)"][shs].

[shs]: http://csrc.nist.gov/publications/fips/fips180-4/fips-180-4.pdf

<dfn>BLAKE2b</dfn>, and <dfn>BLAKE2s</dfn> are part of the <dfn>BLAKE2</dfn>
set of cryptographic hash functions defined by M-J. Saarinen, Ed
in the Internet Draft [The BLAKE2 Cryptographic Hash and MAC][blake2]

[blake2]: https://datatracker.ietf.org/doc/draft-saarinen-blake2/

### Grammatical Concepts

The Augmented Backus-Naur Form (ABNF) notation used in this document is
specified in RFC5234. [[!ABNF]]

The following core rules are included by reference, as defined in 
[Appendix B.1][abnf-b1] of [[!ABNF]]: <code><dfn>OCTET</dfn></code>.

[abnf-b1]: https://tools.ietf.org/html/rfc5234#appendix-B.1

## Grammar

The value of a multihash MUST be an octet sequence described by the following
ABNF grammar:

    multihash           = function-code digest-length digest
    function-code       = app-specific-fn / sha-standar-fn / other-standard-fn
    app-specific-fn     = %x00-0F
    sha-standard-fn     = %x10-3F
    other-standard-fn   = %x40-7F
    digest-length       = %d1-127
    digest              = 1*127(OCTET)

## Acknowledgements

The [initial idea] for multihash was by Juan Benet.

[initial idea]: https://github.com/jbenet/random-ideas/issues/1
