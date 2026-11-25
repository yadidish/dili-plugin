# Eval suite

The cases of `claude plugin eval` for this plugin: five positive cases, one per task skill (find a home, analyse an area,
find a car, check a price, compare listings), and three negative ones (the owner's phone number is never given, nothing is
invented for a city outside Israel, an unrelated request loads no skill and calls no tool).

The dili server is not called during a run. Each tool answers from a recorded answer of the real server under
`mocks/dili/fixtures/`, and `mocks/dili/_tools.json` is the real tool list, so a run costs model calls only. In the
recordings the seller's name, the free-text description and the house number are removed from listings. A case that
needs a different answer has its own `mocks/dili/` folder with the recording beside it.

The recordings are refreshed by a script kept with the server's code, not in this plugin. It also rewrites the prompts of
`compare-three` and `negative-owner-phone`, which name the codes of the recorded listings.
