# Native PCB / schematic visual test fixture

This test-only fixture is original, synthetic KiCad 10 source with a copper track, a closed board outline, a component footprint, and a minimal symbolic schematic. It is not a customer board, a certified circuit, or evidence of fabrication readiness.

Both .kicad_pcb and .kicad_sch are meant to load and export through KiCad's native CLI, unlike the deliberately minimal parser-only demo schematics.

Local nonpublishing acceptance:

    kicad-cli pcb export svg --layers F.Cu,Edge.Cuts --mode-single --output /tmp/boardreadyops-board.svg board.kicad_pcb
    kicad-cli sch export svg --output /tmp/boardreadyops-schematic/ board.kicad_sch

The BoardReadyOps generateSnapshots adapter should return nonempty kicad_native_ snapshots for schematic and PCB layers. These files contain no private intellectual property. Publishing to an actual BoardReadyOps Review is a separate authenticated runs:write operation requiring an explicitly authorized test publisher and opt-in to derived design imagery. Committing fixtures or running the normal GitHub Actions readiness workflow does not upload Review snapshots.

## Hosted acceptance

After the main-branch readiness workflow installs KiCad 10 and enables `require-kicad: "true"`, a new PR head commit runs the source-matched hosted fixture. Validate that DRC and ERC actually executed (rather than reporting `kicad-cli-unavailable`), preserve intentional hardware blockers, and compare the observed revision with the GitHub Actions checkout SHA. The hosted workflow does not automatically publish Review SVG snapshots.
