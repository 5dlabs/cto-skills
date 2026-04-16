The Agent Skills spec (https://agentskills.io/specification) REQUIRES:

  name:        string matching regex ^[a-z0-9]+(-[a-z0-9]+)*$ (lowercase
               alphanumeric + hyphens, no leading/trailing/consecutive
               hyphens), 1-64 chars. MUST EXACTLY EQUAL the parent
               directory name (given above).
               VS Code / GitHub Copilot Chat silently drops skills whose
               `name` does not match the directory — so this is
               non-negotiable.

  description: string, 1-1024 chars, ideally 50-300 chars. Must describe
               BOTH what the skill does AND when an agent should use it.
               Write in third person, imperative mood, no XML tags, no
               "I"/"you" voice. This is what agents read to decide
               relevance — be specific, not generic.

Optional fields you may preserve if already present (do NOT add them
unless the content clearly warrants it):
  license, metadata, compatibility, agents, triggers, llm_docs_url

DO NOT add these Claude-Code-only fields (they're non-portable):
  allowed-tools, model

Rules:
1. Use the Read tool to inspect the target file first.
2. If frontmatter is missing entirely, PREPEND a valid `---` YAML
   block followed by a blank line, then the existing content unchanged.
3. If frontmatter exists, ADD or CORRECT only the fields the validator
   flagged. Do not reorder or remove fields already present.
4. If the current `name` field does not equal the parent directory
   name, change `name` to match the directory (directory is
   authoritative).
5. Infer the description from the file's first heading, opening
   paragraph, or "## Overview" / "## WHAT" section. Target 80-200 chars.
6. Preserve ALL body content below the frontmatter byte-for-byte.
7. Use the Edit tool (or Write if creating the header is easier) to
   apply the change. Do not output a summary — just fix the file.
