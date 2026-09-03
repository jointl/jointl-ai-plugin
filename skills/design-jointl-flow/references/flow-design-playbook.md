# Jointl Flow design playbook

Use this reference after reading the current Flow capability map. Current tool results take precedence over this guide.

## Choose the Flow type

| Flow type | Use for | Core sections |
| --- | --- | --- |
| Hiring Review | Candidates for a defined role | Company and job title, pre-screening, tests or work samples, assessment questions, references, matching attributes |
| Exit Intelligence | Structured departure feedback | Exactly one exit form, focused themes, optional form experience overrides, Flow invitation/reminder copy |
| Performance | Glow Moments recognition and recurring Team Pulse feedback | Shared Employee participants, separate feature enablement/cadence, one Team Pulse form, optional form experience overrides |

## Hiring Review sequence

1. Pre-screening: 3–6 factual, low-burden questions covering required experience, availability, authorization or logistics only when lawful and relevant.
2. Tests: search both the Private and Public Test Library first. Attach each inspected ready-to-use Test that directly measures a material role requirement. If the library has no suitable option, author a focused original Test in `authoredTemplates.assessmentTests` instead of substituting an irrelevant Test. Give every evaluative multiple-choice option an explicit non-negative numeric score with at least two distinct values; keep native scale scoring unless distinct endpoints are intentionally required.
3. Work sample or assessment: put 2–5 high-signal tasks covering realistic decisions, prioritization, analysis, communication, and role craft into the single supported Additional Assessment Question block.
4. References: 1–3 forms suited to the relationship. Inspect reusable Reference content, then use the native structured types where relevant: `strengths` for capabilities plus examples, `keyAchievements` for scope and measurable impact, `weaknesses` for observed development areas and context, `reasonsForLeavingJob` only for the referee's direct knowledge, and `employmentCheck` for formal employer/title/date confirmation. Use each at most once per form and do not duplicate it with a generic long-text question.
5. Matching attributes: choose 4–8 plain-language capabilities and order them deliberately from highest to lowest importance. Jointl applies linear weights N through 1 in that exact order, so never alphabetize them or treat the order as cosmetic. Each must be backed by at least one question that actually emits a numeric score. Use `evidenceRole: evaluative` plus the exact attribute only on supported scored scales or fully scored, non-flat multiple choice. Use `evidenceRole: context` without an attribute for every open-text narrative, logistics, consent, and relationship context. Do not include strengths or weaknesses as scoring attributes.
6. Candidate experience: Public Profiles are on by default; Talent Pool is on by default when the workspace is entitled. Team/public sharing remains off.
7. Human review: leave automated status rules and knockout rules off.

Use short text for precise facts, long text for examples or work samples, and multiple choice only where the choices are genuinely exhaustive. Set `maxAnswers` to the exact limit stated in a multiple-choice prompt; use 1 for single answer and never say “choose up to three” while allowing every option. Open text remains important qualitative evidence but cannot carry a Matching Score attribute; pair a critical narrative with a separate scored question when the same capability must affect the numeric score. Enable AI Follow-Up Question selectively for critical open answers that may need a concrete example, reasoning, scope, or result; leave it off for sensitive or simple factual questions. Enable Insights Extraction only for substantive open-text Reference, Exit Intelligence, and Team Pulse narratives.

Every structured Reference type is qualitative context and must omit `attribute`. `strengths`, `keyAchievements`, `weaknesses`, and `reasonsForLeavingJob` default to Insights Extraction and may selectively enable AI Follow-Up Question when an answer needs evidence depth. `employmentCheck` captures structured employment facts, not a narrative score, and supports neither AI follow-up nor Insights Extraction. These formalized types make downstream reports more consistent; do not replace them with looser prompts when the evidence goal matches.

## Exit Intelligence sequence

1. Inspect `exitIntelligence` library forms and select exactly one when it fits; otherwise author exactly one focused form.
2. Cover departure drivers, the primary trigger, manager support, career growth, role expectations, culture signals, useful retention levers, employer advocacy, and an open final comment. Avoid asking for diagnoses, protected characteristics, or speculation about other Employees.
3. Use rating or opinion-scale questions with attributes for repeatable numeric signals, and open text as attribute-free qualitative context for explanation. Enable AI Follow-Up Question only on a critical narrative that may be vague. Enable Insights Extraction on substantive narratives whose themes should feed Exit Intelligence.
4. Keep the form's native welcome/thank-you experience, conversation mode, and confetti unless a concrete audience or language mismatch justifies an override. Flow invitation/reminder emails are separate settings.
5. Create as DRAFT. Publish only after a separate explicit request. Publishing makes the Flow selectable; it does not contact an Employee.
6. Launch only when the user explicitly marks an Employee left through the confirmed Employee status action, with an end date for every active position and the exact active Exit Intelligence Flow ID.
7. Read individual evidence through Employee detail and cohort themes through Exit Intelligence Insights with the requested inclusive UTC date range.

## Performance sequence

1. Resolve the shared participant set to exact visible Employee IDs. If either feature is enabled, include at least two Employees and ensure every participant has an email. Never infer identities from ambiguous names.
2. Configure Glow Moments independently: enabled or disabled, and when enabled a future one-time cadence or recurring monthly/quarterly cadence. Glow Moments has no form.
3. Configure Team Pulse independently: enabled or disabled, and when enabled a future one-time cadence or recurring monthly/quarterly/semi-annual cadence plus exactly one visible or newly authored Team Pulse form.
4. Team Pulse should cover clarity, workload sustainability, manager support, collaboration, psychological safety, growth, recognition, and an optional open comment. Put attributes on scored rating/opinion-scale signals; keep the open comment attribute-free and qualitative. Keep it compact and suitable for repeated use. Use AI Follow-Up Question only for a critical open narrative and Insights Extraction when that narrative should produce structured themes.
5. Preserve the Team Pulse form's native welcome/thank-you experience, conversation mode, and confetti unless a material mismatch justifies an exact override. Use Flow copy overrides only for Glow or Team Pulse invitation/reminder messages that genuinely need different wording.
6. Create as DRAFT. Publication is a separate confirmed action and schedules the configured features. It does not authorize a manual send-now action.
7. Read cycle state before operating it. A manual Glow Moments or Team Pulse send is its own confirmed action. Cycle cancellation or restoration needs the exact cycle ID and current status from the Performance operations read.
8. Retrieve participant and Glow scoreboard links only when explicitly requested. Treat each returned URL as a bearer capability and warn the user before sharing it.

## Performance design example

```json
{
  "type": "PERFORMANCE",
  "performance": {
    "employeeIds": ["employee-id-1", "employee-id-2"],
    "glowMoments": {
      "enabled": true,
      "cadence": {
        "mode": "RECURRING",
        "firstSendAt": "2026-09-01T09:00:00.000Z",
        "interval": "MONTHLY"
      }
    },
    "teamPulse": {
      "enabled": true,
      "cadence": {
        "mode": "RECURRING",
        "firstSendAt": "2026-09-05T09:00:00.000Z",
        "interval": "QUARTERLY"
      }
    }
  },
  "templateIds": {
    "teamPulse": ["one-exact-template-id"]
  }
}
```

The full input also needs the common title, tag, matching-attribute, authored-template, and copy fields from the current tool schema. Use this only as the type-specific shape; the tool schema takes precedence over the example.

## Candidate-facing copy

Start from Jointl's native welcome, reference, thank-you, invitation, reminder, and completion copy. Override only a field that materially conflicts with the Flow's audience, language, legal context, promised process, or user requirement. Use plain text with supported Jointl placeholders and preserve every unaffected default. On a revision, put an existing overridden field in `clearCopyOverrideFields` only when it should return to Jointl's native copy. Cosmetic rewriting adds review burden without improving the Flow.

## Final quality check

- Every section has a distinct purpose.
- Questions request observable evidence rather than labels or impressions.
- No protected or unnecessarily sensitive data is requested.
- No question tells a model or referee to make the employment decision.
- Relevant Private and Public Library Tests were inspected before any original Test was authored.
- Existing question templates were inspected before reuse.
- Relevant structured Reference types are used at most once per form, remain attribute-free context, and are not duplicated by generic prompts.
- Exit Intelligence has exactly one form and no Performance-only configuration.
- Performance uses exact Employee IDs, at least two participants when enabled, complete future cadence for each enabled feature, no Glow form, and exactly one Team Pulse form when enabled.
- Authored questions are original; every Matching Score attribute has at least one genuinely scoreable question; every open-text narrative is explicitly context with no attribute; narratives are paired with scored questions where the same capability needs numeric impact; and Hiring Review uses at most one Additional Assessment Question block.
- Multiple-choice scoring is explicit and reviewable in every authored form: every evaluative option has a non-negative numeric score with a non-zero range. Test scale scoring is native unless deliberately mapped to distinct endpoints, context questions are unscored, and no Test question requests unsupported AI follow-up or insight extraction.
- Every multiple-choice prompt and its `maxAnswers` limit agree, and Matching Score attributes remain in the intended highest-to-lowest importance order.
- AI Follow-Up Question and Insights Extraction are enabled only where they add evidence depth.
- Public Profiles and, when available for the workspace, Talent Pool have the expected default state.
- Default screens and emails remain unless a specific mismatch justified an override.
- Publishing, manual send, cycle cancellation or restoration, and Employee departure launch remain distinct explicit intents.
- No participant or scoreboard access link is fetched or shared without an exact request and warning.
- Protected settings in the prepare preview are off or unchanged.
- The user sees the full preview before confirmation.
