# kallisto_instrumented (fork)

Instrumented fork of pachterlab kallisto (near-optimal RNA sequencing quantification) with extra tracing/debug outputs for algorithm validation and reimplementations. This fork is for debugging and validation only and is not intended for production use.

Upstream: https://github.com/pachterlab/kallisto

## Instrumentation summary

This fork adds optional debug outputs to trace pseudoalignment internals, per-read EC evolution, per-k-mer decisions, and selected index EC mappings. The outputs are file-based and are only produced when the corresponding flags are provided.

## Changes vs upstream

- Adds optional debug/trace outputs for EC evolution, per-k-mer decisions, minimizer metadata, and hit dumps.
- Adds an index-level EC dump for validating EC mappings and on-list handling.
- Keeps core algorithm behavior intact when debug flags are not used.

## Debug/trace flags (instrumented fork only)

All flags write tab-delimited output to the file path you provide.

- `--ec-trace=FILE` Dump per-read EC tracing with intersection steps and final ECs.
- `--ec-trace-max-reads=INT` Limit EC tracing to the first N reads (0 = all).
- `--hit-dump=FILE` Dump per-read unitig hit details (includes k-mer strings).
- `--ec-dump=FILE` Dump a subset of index k-mers/minimizers and ECs.
- `--ec-dump-limit=INT` Limit the number of k-mers/minimizers dumped (0 = all).
- `--kmer-dump=FILE` Dump every inspected k-mer per read with hit/skip decisions, minimizer flags, and jump info.
- `--kmer-dump-max-reads=INT` Limit k-mer dump to the first N reads (0 = all).

Notes on `--kmer-dump` output fields:
- Includes per-k-mer `hit_action` (`accept`/`skip`) and `skip_reason` (`empty`, `intersection_empty`, or `-`).
- Includes minimizer fields (`minimizer`, `minimizer_pos`, `minimizer_is_special`, `minimizer_is_overcrowded`, `minimizer_is_abundant`, `minimizer_hit_count`) and jump info (`jump_used`, `jump_from_pos`, `jump_to_pos`).

## Not for production use

These tracing paths are for algorithm inspection and validation. They add overhead and are not intended for production quantification or benchmarking.

## kallisto description
_kallisto__ is a program for quantifying abundances of transcripts from
RNA-Seq data, or more generally of target sequences using high-throughput
sequencing reads. It is based on the novel idea of _pseudoalignment_ for
rapidly determining the compatibility of reads with targets, without the need
for alignment. On benchmarks with standard RNA-Seq data, __kallisto__ can
quantify 30 million human bulk RNA-seq reads in less than 3  minutes on a Mac desktop
computer using only the read sequences and a transcriptome index that
itself takes than 10 minutes to build. Pseudoalignment of reads
preserves the key information needed for quantification, and __kallisto__
is therefore not only fast, but also comparably accurate to other existing
quantification tools. In fact, because the pseudoalignment procedure is
robust to errors in the reads, in many benchmarks __kallisto__
significantly outperforms existing tools. The __kallisto__ algorithms are described in more detail in:

NL Bray, H Pimentel, P Melsted and L Pachter, [Near optimal probabilistic RNA-seq quantification](http://www.nature.com/nbt/journal/v34/n5/abs/nbt.3519.html), Nature Biotechnology __34__, p 525--527 (2016).



## License

The project is distributed under the BSD-2 license.
## Getting help

If you need help or want to report issues with this fork, use the fork repository issues page: https://github.com/deminden/kallisto_instrumented/issues
