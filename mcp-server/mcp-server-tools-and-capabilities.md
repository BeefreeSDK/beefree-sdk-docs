# MCP Server tools & capabilities

The Beefree SDK MCP Server provides dozens of tools that are divided into different categories. These tools allow agents to build, modify, and validate email designs in Beefree.

#### Structure and layout tools

These tools control the foundational architecture of your email, allowing you to create sections, manage layouts, configure columns, and set global styles.

* `beefree_add_section` - Add new email sections with column structure
* `beefree_delete_element` - Delete elements from email templates
* `beefree_update_section_style` - Modify section styling
* `beefree_update_column_style` - Modify column styling
* `beefree_get_content_hierarchy` - Retrieve design structure
* `beefree_get_element_details` - Get element information
* `beefree_set_email_metadata` - Set email subject and preheader
* `beefree_set_email_default_styles` - Set default email styles

#### Get the context of selected element

```
const beeConfig = {
  onSelectElement: ({type, uuid}) => {}
}
```

The `onSelectElement` callback is triggered when a user selects either a row or a module in the SDK interface. It is called with an object parameter that contains:

* a `type` field, which can be either `module` or `row`
* a `uuid` field, which contains the ID of the selected element

This information is meant to be forwarded to your AI Agent that can proactively leverage them in MCP-powered content creation.

#### Design system & personalization

These features work across multiple tools and categories to ensure designs are personalized and responsive.

* **Mobile styles**: Specialized styling tools to control how layouts and content appear on smaller screens (e.g., stacking, padding, and visibility).
* **Merge tags**: Dynamic placeholders used across text-based components to enable 1-to-1 personalization.

#### Content block tools

These tools add and modify individual content elements within your email, including text, images, buttons, and other interactive components.

* Text blocks: `beefree_add_title`, `beefree_add_paragraph`, `beefree_add_list`
* Media blocks: `beefree_add_image`, `beefree_add_icon`
* Interactive blocks: `beefree_add_button`, `beefree_add_social`, `beefree_add_menu`
* Structural blocks: `beefree_add_spacer`, `beefree_add_divider`
* Tabular blocks: `beefree_add_table`
* Each with corresponding update tools

#### Validation & QA tools (Checker)

These tools verify email quality by checking for accessibility issues, missing alt text, color contrast problems, broken links, and other best practice violations.

* `beefree_check_template` - Template validation
* `beefree_check_section` - Section validation

#### External services

These tools integrate with third-party services to enhance your email designs with external resources and assets.

The Beefree SDK MCP server uses the [Pexels API](https://www.pexels.com/api/).

* `beefree_search_stock_images` - Retrieve stock images via Pexels API integration. Search for high-quality, royalty-free images to use in your email designs. Returns image URLs, descriptions, and attribution information.

With each of the tools in the categories above, agents can build complete workflows: from inserting content, to structuring layouts, to validating designs against accessibility and best practices.

#### Actions Available on Blocks

The table below outlines the specific operations (Add, Read, Update, and Delete) that AI agents can perform on various content blocks within the editor via the Beefree SDK MCP server. Use this reference to understand the current capabilities and functional coverage available for each block type.

<table><thead><tr><th>Block</th><th data-type="checkbox">ADD</th><th data-type="checkbox">READ</th><th data-type="checkbox">UPDATE</th><th data-type="checkbox">DELETE</th></tr></thead><tbody><tr><td>Button</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Paragraph</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Heading</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Image</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Divider</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Spacer</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>List</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Icon</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Social</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Text</td><td>false</td><td>true</td><td>false</td><td>true</td></tr><tr><td>Menu</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Dynamic Content</td><td>false</td><td>false</td><td>false</td><td>true</td></tr><tr><td>HTML</td><td>false</td><td>false</td><td>false</td><td>true</td></tr><tr><td>Table</td><td>true</td><td>true</td><td>true</td><td>true</td></tr><tr><td>Video</td><td>false</td><td>true</td><td>false</td><td>true</td></tr></tbody></table>
