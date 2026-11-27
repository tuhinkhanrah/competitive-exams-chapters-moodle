# competitive-exams-chapters-moodle

Chapter-wise Moodle outputs are stored in a directory named after the source
chapter code. For example, outputs generated from `kebo101.pdf` go in
`neet-ug/ncert/class11/biology/kebo1dd/kebo101/`. Book-level files stay in the
parent book directory.

For other source filenames, the existing question runner writes beside the
mirrored source parent, while tutorials use a chapter-stem subdirectory. The
shared index understands both layouts; existing assets do not need moving.

## Offline chapter index

`chapter-index.json` is a generated snapshot, not another editable source
catalog. Rebuild to a **new filename** with
[`academic_content_pipeline.chapter_index`](../academic-content-pipeline/README.md#shared-chapter-sources-and-offline-index),
then review the diff before replacing a versioned snapshot. It includes all
recognized source chapters, even when titles or generated assets are missing,
and requested English/bilingual variants. References/checksums are relative to
the source or artifact repository; machine-specific absolute paths and secrets
are excluded.

Existing mapped OCR Markdown supplies NEET chapter titles without OCR or AI.
New generation writes `.source.json` sidecars; historical outputs without these
remain explicitly unverified rather than being retroactively certified.
Question-type manifests remain authoritative for planned/completed files and
saved XML checksums. Missing files, checksum drift, incomplete counts and
placeholders are surfaced as readiness issues. The index does not rewrite
question types/grades or modify existing generated assets.

The Moodle repository's
[course generator](../bosonance-moodle-site/scripts/course-template-generator/README.md)
consumes the index to produce reviewable YAML drafts.

The three `chapter-index-*-syllabus.review.json` snapshots index
the JEE Main, JEE Advanced and WBJEE source trees, including their separate
`workflow-fixtures` fixtures. Select `syllabus` explicitly when
generating proposals. These snapshots record title-only placeholders and
missing content; they do not certify official syllabus coverage.

The NEET `chapter-index-neet-reviewed-order.review.json` and
`chapter-index-neet-exemplar-reviewed-order.review.json` snapshots include
source-hashed chapter-order manifests and the newly available Class 12 p-block
PDF. Its title and Exemplar association are still unresolved.

## NCERT Exemplar associations

[`ncert-exemplar-map.json`](./ncert-exemplar-map.json) is the resolved,
source-hashed snapshot of the
[maintained crosswalk](../competitive-exams-chapters/ncert-exemplar-crosswalk.yaml):
80 current `ncert` chapter sources are matched, including the confirmed Class 11
p-block NEET supplement. All 97 Exemplar PDFs are accounted for; 17 have
no standalone counterpart in the selected textbook source set.

Chapter source paths are relative to `competitive-exams-chapters`; Exemplar
source paths are relative to
`question-papers-vault/ncert-exemplar-question-bank`. The source crosswalk
contains stable IDs only; these paths/checksums are derived by the
[pipeline resolver](../academic-content-pipeline/README.md#ncert-exemplar-crosswalk).
Rebuild to a new filename, review differences, and then replace the snapshot.
This file is not an Exemplar XML inventory or an executable quiz-import plan.
Different language-specific question counts do not affect associations.
The `ncert` source set may intentionally contain old NCERT supplements required
by NEET. The Class 12 p-block PDF is present but its Exemplar mapping remains
unresolved; absence from newer textbooks is not itself a syllabus-exclusion rule.

[`chapter-index-exemplar.json`](./chapter-index-exemplar.json) extends the
chapter inventory with mapped Exemplar XML/checkpoint references for each
language. It currently contains 240 ready Exemplar inventories across 80
`ncert` chapters. The original `chapter-index.json` remains a separate older
snapshot; reviewed proposals are not overwritten automatically.

In the extended index, Exemplar PDF references are relative to the input
`question-papers-vault/ncert-exemplar-question-bank` root, and XML/checkpoint
references to its corresponding output root in `question-papers-vault-moodle`.
The consumer must configure both roots explicitly. Map-approved titles are
used only when the current chapter source hash matches, with provenance
`reviewed-exemplar-crosswalk`. Readiness covers structural/source integrity,
not Moodle parser compatibility or question-level syllabus approval.

## Question bank category exports

The `question_bank_categories` directory contains the exam-specific XML files
split from `bosonance_leaf_categories.xml`: JEE Advanced, JEE Main, NEET (UG),
and WBJEE.
