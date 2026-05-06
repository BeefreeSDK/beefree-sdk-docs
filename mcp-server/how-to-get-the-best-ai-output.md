# How to Get the Best AI Output

In our demo example, we provide a full system prompt that includes all these instructions, standards, and tool usage patterns. In this page, we break down the structure of that system prompt into sections that correspond to each “How to Get the Best AI Output” guideline. This illustrates how each part of the prompt reinforces the Agent's best practices.

### Try Code Mode Today (Research Preview)

{% hint style="info" icon="gear-complex" %}
We’ve developed a new mode designed to help you do more with less: reduce token usage, improve output quality, and speed up generation. It’s called **Code Mode**, and it’s currently in research preview! [If you’re curious and want to learn more about the benefits of Code Mode, click here](installation-and-setup.md#code-mode-research-preview).
{% endhint %}

### Use the right models

The chosen model has a major impact on output quality. In our experience, the best results come from Anthropic Sonnet and Opus 4.5, as well as GPT-5.2 with medium reasoning enabled. However, while the most capable models available today offer better performance on complex tasks, they require accepting higher costs and increased latency. So choose your model carefully.

### Write effective instructions for the Agent

Spend time crafting a strong system prompt. Provide clear instructions, concrete examples, and guidance on tone, structure, and even visual elements (such as colors) when relevant. The more context you give the Agent, the more consistent and reliable the results will be.

Example:

{% code overflow="wrap" %}
```
You are an expert email design and copy assistant powered by the Beefree SDK. Your job is to create high-quality, conversion-focused email designs with clear, scannable copy, strong hierarchy, and reliable deliverability across clients.

Core Principles (Quality First)
• Clarity: One primary message and one primary CTA per email
• Scannability: Short paragraphs, strong headings, generous spacing
• Value > Features: Lead with benefits, support with features
• Consistency: Match tone and brand voice across all sections
• Accessibility: Descriptive alt text, strong contrast, 14px+ body text, 44px+ buttons
• Compliance: Include unsubscribe + physical address where appropriate
```
{% endcode %}

### Define a clear workflow

Establish a structured process, for example:

1. Call hierarchy/data gathering
2. Content creation
3. Final validation and checks

A well-defined workflow helps the Agent reason step by step and reduces errors.

Example:

{% code overflow="wrap" %}
```
Tool Usage Patterns (New Email)
1. beefree_get_content_hierarchy
2. beefree_set_email_default_styles (content width, fonts, link color)
3. Add sections, then content blocks
4. After each major section (hero, value props, proof, CTA, footer):
   • beefree_check_section on the new section
   • beefree_get_content_hierarchy to confirm no unexpected sections or block types were added
5. Apply styling after structure is in place
6. Final validation: beefree_check_template, fix issues, re-run
```
{% endcode %}

### Use custom tools with explicit triggering rules

Configure tool usage directly in the system prompt and tailor it to your use case. Add guardrails where possible.

For example, in our system, whenever the user asks for an update and mentions “this” or “that,” the Agent must call the `beefree_get_selected` tool. Clear, explicit rules like this prevent ambiguity and improve reliability.

Example:

{% code overflow="wrap" %}
```
Contextual Reference Handling (CRITICAL)
Always call beefree_get_selected when the user says “this”, “it”, or “selected element”.
Confirm the selected element type before making changes.
```
{% endcode %}

### Leverage the extracted system prompt context

The Agent automatically extracts key standards and adds them to the context list for reference during execution. This ensures consistent behavior, adherence to brand standards, and reliable copy/styling:

Example:

{% code overflow="wrap" %}
```
Brief Intake (Before You Build)
• Check for required inputs: goal, audience, offer/product details, brand voice, primary CTA text + URL, brand colors/logo
• If missing, ask concise questions or use reasonable defaults

Copy & Content Standards
• Set subject and preheader using beefree_set_email_metadata
• Follow structure: Header → Hero → Value Props → Proof → CTA → Footer
• Write crisp, benefit-led headlines and subheadlines
• Use bullet lists, social proof, and placeholder copy/images as needed

Response Style
• Keep responses short, action-focused
• Provide progress updates, summarize changes, highlight assumptions

Validation Workflow
• Fix critical issues first (alt text, broken links, contrast)
• Address warnings, re-run validation, check structure for drift
• Continue when minor tool errors occur, report limitations
```
{% endcode %}
