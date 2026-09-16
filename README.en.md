![Chinese Writing: clearer Chinese, with attention to facts and author voice](assets/social-preview.svg)

# Chinese Writing

[中文](README.md) · **English** · [MIT](LICENSE)

An Agent Skill for drafting and editing Chinese text, with attention to facts, qualifications, and the author's voice.

Use it for emails, product notes, reports, and academic paragraphs. It gives an assistant instructions for revising vague claims, awkward phrasing, and repetition while leaving already natural writing alone.

It works in tools that read `SKILL.md`, such as Claude Code and Codex. Other tools that support Agent Skills follow their own installation docs. The install command is under [Quick start](#quick-start).

## Three editing examples

These are **fictional examples** from the repository, illustrating the intended editing behavior. They are not real product results or research findings. All numbers come from the respective source drafts.

### Product note: keep the evidence specific

**Before**

> 此次升级不仅是一次功能迭代，更是一次效率革命。系统现已支持批量导入CSV文件。在20名内测用户中，完成同一项导入任务的中位耗时从10分钟降至6分钟。批量导出尚未上线。

**After**

> 系统现已支持批量导入CSV文件。20名内测用户完成同一项导入任务的中位耗时从10分钟降至6分钟。批量导出尚未上线。

The inflated claim is removed. The sample of 20 testers, median task time, and unavailable export feature remain.

### Email: make the request clear

**Before**

> 为切实推动项目协同工作的高效开展，现将修订后的方案同步给您。烦请您于周四前审阅第二部分，并就预算安排提出宝贵意见。

**After**

> 修订后的方案发您了。烦请您在周四前看一下第二部分，并对预算安排提些意见。

The request, review scope, deadline, and courtesy remain. No new promise is added.

### Academic paragraph: keep the limits of the finding

**Before**

> 值得强调的是，我们的实证结果在一定程度上揭示了企业采用该工具与处理时间之间的复杂关系。估计系数为−0.08，标准误为0.06，未达到常用显著性水平。这一结果尚不足以支持因果解释。

**After**

> 我们考察了企业采用该工具与处理时间的关系。估计系数为−0.08，标准误为0.06，未达到常用显著性水平。该结果尚不足以支持因果解释。

The coefficient, standard error, lack of statistical significance, and causal limitation remain. See [more examples](skills/chinese-writing/references/examples.md) in Chinese.

## Quick start

With the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add Chase-Chen1999/chinese-writing-skill --skill chinese-writing
```

On 2026-09-14, a Codex project-level copy installation was checked with Skills CLI 1.5.26 and `--agent codex --copy --yes`. All three installed skill files matched the source files. Model auto-activation was not tested.

## Manual installation and prompt use

For manual installation, download this repository and copy the entire [skills/chinese-writing](skills/chinese-writing) directory into your tool's skills directory. Keep the `references` and `agents` subdirectories so relative links work. Follow your tool's documentation for the installation location and activation behavior.

To try the instructions as a prompt, copy the body of [SKILL.md](skills/chinese-writing/SKILL.md) after its YAML frontmatter. Include [examples.md](skills/chinese-writing/references/examples.md) when you need the additional examples.

## Copy a prompt

**Edit a draft**

```text
Use $chinese-writing to edit the Chinese text below. Preserve numbers, direct quotes, and qualifications. Return the edited text:
[draft]
```

**Draft from notes**

```text
Use $chinese-writing to write a polite, natural Chinese email to a colleague from these notes. Do not add commitments I have not made:
[notes]
```

**Match your voice**

```text
Use $chinese-writing to revise the new Chinese draft in the voice of my two writing samples. Use the samples for style only; do not transfer their facts into the draft:
[writing samples]
[new draft]
```

`$chinese-writing` is one explicit invocation form. Adjust it if your tool uses a different skill syntax.

## Editing rules and limits

- Make small edits by default; restructure when the user asks for a substantial rewrite.
- Identify numbers, units, direct quotes, negations, conditions, and commitments before editing, then check against the source.
- Judge rhetoric in context. Avoid mechanical word bans or invented experiences added for personality.
- Editing is not fact-checking. Authors should review the output. The skill makes no AI-detector score or detection-avoidance promise.

The full instructions are in [SKILL.md](skills/chinese-writing/SKILL.md). The skill is mainly Markdown and has no accompanying execution scripts. Its behavior depends on the model reading and following the instructions in your tool.

## Checks so far

The [six synthetic smoke cases](evals/cases.md) cover statistical interpretation, plans versus results, email commitments, avoiding unnecessary edits, quotes and style samples, and contradictory numbers.

One round was run in an independent assistant session and manually reviewed by the maintainer. Read the [outputs and review notes](evals/smoke-test.md). This small behavioral check is not a cross-model benchmark or a comparison with other humanizers.

## Give feedback

[Open an issue](https://github.com/Chase-Chen1999/chinese-writing-skill/issues/new) with a draft, the actual output, what should have been preserved, and the tool and model used. Remove private information before posting publicly.

## Related projects and provenance

| Project | Focus explored during research |
| --- | --- |
| [blader/humanizer](https://github.com/blader/humanizer) | English editing and review of AI writing patterns. |
| [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) | Chinese translation and adaptation of humanizer. |
| [zdyya/writer-skill](https://github.com/zdyya/writer-skill) | A workflow for planning, researching, writing, and reviewing Chinese long-form text. |

These projects were comparison points during initial research. This repository's skill text and Chinese examples were written afresh, rather than translated paragraph by paragraph or assembled from their rules. No endorsement by their authors is implied.

## License

[MIT](LICENSE).
