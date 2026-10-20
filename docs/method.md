# Method overview

ByteDistill compares language-model predictions at shared positions in decoded text, even when the teacher and student use different tokenizers. The comparison space is the 256 possible UTF-8 byte values. Byte-Level Distribution Alignment (BLDA) is the resulting distillation loss.

## Aligned chunks

The same response is tokenized separately by the teacher and student. Each token occupies an interval of byte positions. Connected groups of overlapping intervals form chunks that cover the same substring on both sides, while allowing different internal token boundaries.

At a shared byte position, each model retains its own native token history and the byte prefix matched within its candidate tokens. These histories and prefixes can differ between models.

## Next-byte distributions

For a selected native state, ByteDistill sums the probabilities of textual candidate tokens by their next byte after the matched prefix.

- **Inside an observed token:** normalize the mass of candidates that continue the matched prefix.
- **At an observed token boundary:** combine continuation mass from longer candidates with the mass of ending the observed token, distributed according to the next native state's byte distribution.

The second case uses the state reached by consuming the observed token. The paper calls this **observed-path closure**. It does not marginalize over all token histories compatible with the decoded text. KL is computed between the resulting normalized byte distributions; this is not a claim of exact marginalization over every possible tokenization path.

A position contributes to the loss only when both models pass the validity checks, including positive normalization mass and a valid next state when needed. At a boundary, the observed token must be the unique textual token with that byte string after canonicalization.

## Training objectives

Both byte distributions are smoothed with a uniform distribution before comparison. Only the student is updated.

| Setting | Responses | Byte-level objective |
| --- | --- | --- |
| Off-policy | Fixed responses | Forward KL, `KL(teacher ∥ student)`, combined with the student's next-token SFT loss |
| On-policy | Responses sampled from the current student, then retokenized by both models | Reverse KL, `KL(student ∥ teacher)` |

On-policy gradients flow through the student distributions, not through response sampling or retokenization.

## Scope

BLDA compares textual byte probabilities conditional on continuing the text stream. Structural tokens such as EOS and chat-template markers have no shared byte representation and are excluded from these comparisons. Off-policy training learns their behavior through the SFT loss; on-policy training retains the behavior from SFT initialization and the prompt template.

This page describes the paper's method. The implementation and runnable recipes are pending release.
