Write your CV or resume as YAML, then run RenderCV,

rendercv render John_Doe_CV.yaml

and get a PDF with perfect typography.

With RenderCV, you can:

- Version-control your CV — it's just text.

- Focus on content — don't worry about the formatting.

- Get perfect typography — consistent alignment and spacing, handled for you.

A YAML file like this:

cv:
  name: John Doe
  location: San Francisco, CA
  email: john.doe@email.com
  website: https://rendercv.com/
  social_networks:
    - network: LinkedIn
      username: rendercv
    - network: GitHub
      username: rendercv
  sections:
    Welcome to RenderCV:
      - RenderCV reads a CV written in a YAML file, and generates a PDF with professional typography.
      - See the [documentation](https://docs.rendercv.com) for more details.
    education:
      - institution: Princeton University
        area: Computer Science
        degree: PhD
        date:
        start_date: 2018-09
        end_date: 2023-05
        location: Princeton, NJ
        summary:
        highlights:
          - "Thesis: Efficient Neural Architecture Search for Resource-Constrained Deployment"
          - "Advisor: Prof. Sanjeev Arora"
          - NSF Graduate Research Fellowship, Siebel Scholar (Class of 2022)
    ...

becomes one of these PDFs. Click on the images to preview.

RenderCV's JSON Schema lets you fill out the YAML interactively, with autocompletion and inline documentation.

[](https://raw.githubusercontent.com/rendercv/rendercv/main/docs/assets/images/json_schema.gif)

You have full control over every detail.

design:
  theme: classic
  page:
    size: us-letter
    top_margin: 0.7in
    bottom_margin: 0.7in
    left_margin: 0.7in
    right_margin: 0.7in
    show_footer: true
    show_top_note: true
  colors:
    body: rgb(0, 0, 0)
    name: rgb(0, 79, 144)
    headline: rgb(0, 79, 144)
    connections: rgb(0, 79, 144)
    section_titles: rgb(0, 79, 144)
    links: rgb(0, 79, 144)
    footer: rgb(128, 128, 128)
    top_note: rgb(128, 128, 128)
  typography:
    line_spacing: 0.6em
    alignment: justified
    date_and_location_column_alignment: right
    font_family: Source Sans 3
  # ...and much more

[](https://raw.githubusercontent.com/rendercv/rendercv/main/docs/assets/images/design_options.gif)

No surprises. If something's wrong, you'll know exactly what and where. If it's valid, you get a perfect PDF.

[](https://raw.githubusercontent.com/rendercv/rendercv/main/docs/assets/images/validation.gif)

Fill out the locale field for your language.

locale:
  language: english
  last_updated: Last updated in
  month: month
  months: months
  year: year
  years: years
  present: present
  month_abbreviations:
    - Jan
    - Feb
    - Mar
  ...

Let AI coding agents create and edit your CV. Install the RenderCV skill:

npx skills add rendercv/rendercv-skill

Works with any AI agent that supports the [skills standard](https://skills.sh). The skill is [auto-generated](https://github.com/rendercv/rendercv/blob/main/scripts/rendercv_skill/generate.py) from RenderCV's source code and [evaluated](https://github.com/rendercv/rendercv/tree/main/scripts/rendercv_skill/evals) with promptfoo against RenderCV's own Pydantic validation pipeline. See the [documentation](https://docs.rendercv.com/user_guide/how_to/use_the_ai_agent_skill) for details.

Install RenderCV (Requires Python 3.12+):
```
pip install "rendercv[full]"

```

Create a new CV yaml file:

Edit the YAML, then render:
```
rendercv render "John_Doe_CV.yaml"

```

For more details, see the [user guide](https://docs.rendercv.com/user_guide/).