---

# The YAML header is required for IBM CLoud Docs.
# For more information about the YAML, see
# https://test.cloud.ibm.com/docs/writing?topic=writing-reference-architectures

copyright:
  years: 2023
lastupdated: "2023-01-30"

keywords:

subcollection: # From your toc.yaml file in IBM Cloud Docs

authors:
  - name: "author1"
    url: "https://www.example.com/profile/author1"
  - name: "author2"
    url: "https://www.example.com/profile/author2"

# The release that the reference architecture describes
version: 1.0

# Use if the reference architecture has deployable code.
# Value is the URL to land the user in the IBM Cloud catalog details page
# for the deployable architecture.
# See https://test.cloud.ibm.com/docs/get-coding?topic=get-coding-deploy-button
deployment-url: url

docs: https://cloud.ibm.com/docs/solution-guide

image_source: https://github.com/terraform-ibm-modules/module/reference-architectures/xxx.svg

related_links:
  - title: 'Title'
    url: 'https://url.com'
    description: 'Description.'
  - title: 'related or follow-on architectures'
    url: 'https://url'
    description: 'Description'

# use-case from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/subsets/use_cases/use_cases_flat_list.csv
use-case:

# industry from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/industries/industry_sectors%20-%20flat%20list.csv
industry:

# compliance from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/compliance_entities/compliance_entities_flat_list.csv
compliance:

content-type: reference-architecture

---

<!--
The following line inserts all the attribute definitions. Don't delete.
-->

{{site.data.keyword.attribute-definition-list}}

<!--
Don't include "reference architecture" in the following title.
Specify a title based on a use case. If the architecture has a module
or tile in the IBM Cloud catalog, match the title to the catalog. See
https://test.cloud.ibm.com/docs/solution-as-code?topic=solution-as-code-naming-guidance.
-->

# Title
{: #title-id}
{: toc-content-type="reference-architecture"}
{: toc-industry="value"}
{: toc-use-case="value"}
{: toc-compliance="value"}

<!--
The IDs, such as {: #title-id} are required for publishing this reference
architecture in IBM Cloud Docs. Set unique IDs for each heading. Also include
the toc attributes on the H1, repeating the values from the YAML header.
 -->

<!--
All reference architectures stored in the /reference-architectures directory
are published in the IBM Cloud Docs. For more information about this template,
see https://test.cloud.ibm.com/docs/writing?topic=writing-reference-architectures
-->

Include a short description, summary, or overview in a single paragraph that follows the title.

## Architecture diagram
{: #architecture-diagram}

Include the architecture diagram SVG file that was created by using drawio and the IBM2 library. Publishing in IBM Cloud Docs requires that the diagram is stored in the `reference-architectures` directory.


![Enter image alt text here.](example-architecture-diagram.svg "Title text that shows on hover here"){: caption="Figure 1. A description that prints on the page" caption-side="bottom"}

## Design requirements
{: #design-requirements}

Customize the design requirement heat map template image and highlight the scope of the architecture. Publishing in IBM Cloud Docs requires a caption to meet accessibility requirements.

![Enter image alt text here.](heatmap.svg "Title text that shows on hover here"){: caption="Figure 1. A description that prints on the page" caption-side="bottom"}

For more information about creating a design requirements heat map image, see [Design requirements heat map](https://test.cloud.ibm.com/docs/architecture-framework?topic=architecture-framework-heat-map).

After the heat map image, include in this section a write up of the typical use case for the architecture. The use case might include the motivation for the architecture composition, business challenge, or target cloud environments.

## Components
{: #components}

The listing of components and their purpose in the architecture should include what requirement the component meets, what component was chosen for this architecture, the reasons for the choice, and any alternative choices considered. These alternative choices _should_ be components or modules that are tested to swap out.

If the architecture is large and includes several rows of the heat map, consider grouping each row in the design requirements heat map as an H3 section. Include a table for just that row where the caption represents that title. For example, `### Security decisions`. Otherwise, use a single table and now subsections.


| Requirement | Component | Reasons for choice | Alternative choice |
|-------------|-----------|--------------------|--------------------|
|             |           |                    |                    |
{: caption="Table 1. Architecture decisions" caption-side="bottom"}

If you use callout values for components in the architecture diagram, include the value in the table row and component cell that covers it. This guideline applies only if you're publishing to IBM Cloud Docs.

## Compliance
{: #compliance}

_Optional section._ Feedback from users implies that architects want only the high-level compliance items and links off to control details that team members can review. Include the list of control profiles or compliance audits that this architecture meets. For controls, provide "learn more" links to the control library that is published in the IBM Cloud Docs. For audits, provide information about the compliance item.

## Next steps
{: #next-steps}

Optional section. Include links to your deployment guide or next steps to get started with the architecture.

:exclamation: **Important:** Rename this file `<architecture-name>.md`. In the case of deployable architectures, `<architecture-name>` is the same as the deployable architecture name.
