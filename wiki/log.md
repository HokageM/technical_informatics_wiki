# Log

Append-only chronological record of ingests, queries, and lint passes.
Format: `## [YYYY-MM-DD] ingest|query|lint | <title>`

## [2026-10-25] setup | Wiki initialized

- Created CLAUDE.md schema, wiki/ and raw/ directory structure.
- Awaiting first handwritten summary to ingest.

## [2026-10-25] ingest | ti_1.pdf (Boolean algebra through finite state machines)

- Source: raw/summaries/ti_1.pdf (32 pages: lecture notes + exercise sheets Blatt 1-6)
- Pages created: [[topics/boolean-algebra]], [[topics/switching-functions-and-gates]], [[topics/combinational-circuits-mux-demux]], [[topics/flip-flops-and-sequential-logic]], [[topics/finite-state-machines]], [[topics/electronic-devices-and-memory]], [[concepts/karnaugh-map]], [[concepts/functional-completeness]]
- Notes: translated from German handwritten notes. One intermediate algebra step on the NAND-gate-count exercise (p.8) was partly illegible but the final result was clear. Covers: Boolean algebra laws, minterms/maxterms, DNF/CNF, Karnaugh maps, logic gates incl. NAND/NOR functional completeness, multiplexers/demultiplexers/encoders/decoders, RS/D/JK/T flip-flops, shift registers, Moore/Mealy automata and conversion, and a short electronics/memory wrap-up (diodes, transistors, MOSFETs, ROM family).

## [2026-10-25] ingest | ti_2.pdf (Binary arithmetic, exercise FSMs, computer architecture)

- Source: raw/summaries/ti_2.pdf (30 pages: exercise sheets Blatt 6-8 + lecture notes)
- Pages created: [[topics/binary-arithmetic-and-adders]], [[topics/computer-architecture-and-isa]]
- Pages updated: [[topics/finite-state-machines]] (added vending-machine and sensor-alarm worked examples)
- Notes: translated from German handwritten notes. Blatt 6 covers two's-complement numbers/overflow, half/full/N-bit adders, binary multiplication (school method), Booth's algorithm for signed multiplication, and restoring division, all with multiple worked numeric examples. Blatt 7 starts with two FSM design exercises (vending machine Moore automaton; sensor-based alarm system) folded into finite-state-machines.md, then pivots to a new lecture topic: computer architecture (Stone and Amdahl/Blaauw/Brooks definitions, internal vs. external architecture, Von Neumann model, addressing granularity, n-address machine styles 3/2/1.5/1/0-address, RPN/UPN and expression trees, instruction groups). Blatt 8 adds a pipelining throughput exercise and a CISC vs. RISC comparison (CPI, program runtime formula). One table in the n-address-machine addressing exercise (p.29, the `n=2` row) was illegible/crossed out — flagged in the computer-architecture page's open questions.

## [2026-10-25] ingest | ti_3.pdf (MIPS pipeline hazards, CRC, memory hierarchy, virtual memory & caching)

- Source: raw/summaries/ti_3.pdf (30 pages: lecture notes + exercise sheets Blatt 9-12)
- Pages created: [[topics/mips-pipeline-and-hazards]], [[topics/error-detection-crc]], [[topics/virtual-memory-and-caching]]
- Pages updated: [[topics/electronic-devices-and-memory]] (added memory hierarchy, SRAM/DRAM cell structure and trade-offs)
- Notes: translated from German handwritten notes. Blatt 9 covers the 5-stage MIPS pipeline (IF/ID/EX/MEM/WB), stalls vs. flushes, RAW/WAR/WAW data hazards (incl. a 5x5 dependency-matrix exercise), hazard detection via NOP insertion, branch resolution in ID, and forwarding/bypass paths. Blatt 10 covers CRC error detection (polynomial division, CRC-5/CRC-7 worked examples, burst-error detection bound of degree n-k). Lecture notes between exercises cover the memory hierarchy pyramid and SRAM (flip-flop-based) vs. DRAM (capacitor-based, RAS/CAS addressing, refresh) — folded into the existing electronic-devices-and-memory page. Blatt 11-12 cover virtual memory/paging/TLB and direct/n-way-associative/fully-associative cache mapping, plus a worked cache-address-bit-breakdown exercise. Flagged two minor gaps: an illegible cell in a prior addressing-exercise table (noted on the computer-architecture page) and an unclear link between a mux/demux gate-count exercise and the cache-mapping discussion on the same sheet (noted on the virtual-memory page).

## [2026-10-25] ingest | ti_4.pdf (Cache policies/coherence, line coding, I/O and buses)

- Source: raw/summaries/ti_4.pdf (14 pages: remainder of Blatt 12 + Blatt 13 + I/O/bus lecture notes)
- Pages created: [[topics/line-coding-and-signal-encoding]], [[topics/io-systems-and-buses]]
- Pages updated: [[topics/virtual-memory-and-caching]] (added page-replacement algorithms FIFO/LRU/Clock, write-through vs. copy-back write policies, virtual-vs-real cache trade-offs incl. context-switch and synonym problems, and bus-snooping cache coherence)
- Notes: translated from German handwritten notes. Blatt 12 continues with a worked FIFO/LRU/Clock cache-replacement comparison, then lecture notes cover write-through vs. copy-back write policies, virtual vs. real cache placement (and their respective context-switch/synonym/sharing trade-offs), and bus-snooping cache coherence — all folded into virtual-memory-and-caching.md. Blatt 13 covers line coding (NRZ vs. NRZI) for SATA/USB signals, incl. the clock-synchronization problem and USB's bit-stuffing fix (insert a 0 after 6 consecutive 1s). The final lecture section covers I/O systems: memory-mapped vs. separate I/O address spaces, synchronous vs. asynchronous buses, unidirectional vs. bidirectional transfer trade-offs, status-polling vs. interrupt-driven I/O, DMA (device as bus master), and bus topologies/arbitration (daisy-chain vs. parallel/central, avoiding short circuits and bus starvation). This completes the full ingest of all four raw sources (ti_1-ti_4.pdf).
