# cbor-tag-text-key-map

This document proposes a CBOR tag for maps having text-only keys.

**Status**: **Request pending**.

**Proposed tag value**: 275

**Data item**: Map (major type 5)

**Semantics**: Map contains only keys that are of type Text String (major type 3)

## Rationale

When converting from CBOR to JSON, a sensible way to handle CBOR maps with non-text keys would be to output them as arrays of pairs.  A Javascript decoder consuming the JSON conversion may then interpret the array of pairs as a Map.

When the input map contains only text keys, it may be preferrable to output a JSON Object instead of an array of pairs, so that a Javascript decoder may interpret it directly as an Object.

The problem with this approach is that a stream-based CBOR-to-JSON converter cannot determine a priori if the input CBOR map contains only text keys. Once it has begun encoding an output Object, it cannot change the output representation once it encounters a non-text key in the input CBOR map.

With the proposed tag, it would be possible for a stream-based CBOR-to-JSON converter to determine a priori if an input CBOR map contains only text keys, and thus encode it directly to a JSON Object without having to first process the entire input map.
