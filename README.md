# network_diagram_standards
FOSS Network Diagramming standards. Created by Blair Bryant. Free to use.

# Network Diagram Design System Standards
Version 1.8 | February 2025

## Table of Contents
1. [Purpose](#purpose)
2. [Core Principles](#core-principles)
3. [Visual Standards](#visual-standards)
4. [Layer 2 Standards](#layer-2-standards)
5. [Layer 3 Standards](#layer-3-standards)
6. [Layout & Spacing](#layout--spacing)
7. [Typography](#typography)
8. [Tool-Specific Implementations](#tool-specific-implementations)
9. [Documentation Requirements](#documentation-requirements)
10. [Best Practices](#best-practices)
11. [Quality Control](#quality-control)
12. [Accessibility](#accessibility)
13. [Security Considerations](#security-considerations)

## Purpose
This document establishes a unified design system for creating network diagrams across all tools and platforms. By following these standards, organizations ensure consistency, clarity, and maintainability of network documentation, enabling easier collaboration and faster troubleshooting.

## Core Principles
- **Use only circles, squares, and clouds:**  This simplifies visual interpretation and avoids unnecessary complexity, making diagrams easier to understand at a glance.
- **Maintain simple two-size system:**  Limiting sizes improves consistency and makes it easier to judge the relative importance of elements.
- **Apply uniform color scheme:** Consistent colors allow for quick identification of network element types.
- **Keep typography consistent and simple:**  Uniform typography ensures readability and a professional appearance.
- **Ensure accessibility through contrast patterns:**  Meeting accessibility standards ensures that diagrams are usable by everyone, including those with visual impairments.
- **Keep diagrams tool-agnostic:**  Focusing on fundamental visual elements ensures diagrams can be created and understood regardless of the specific software used.

## Visual Standards

### Shape, Size & Color System

| Network Element | Shape | Size | Color (Hex) | Border Color | Border Width |
|----------------|-------|------|-------------|--------------|--------------|
| Core Router | Circle | Large | #4A90E2 | #000000 | 1pt |
| Core Switch | Circle | Large | #7ED321 | #000000 | 1pt |
| Firewall | Square | Large | #D0021B | #000000 | 1pt |
| Server | Square | Small | #4A4A4A | #000000 | 1pt |
| Load Balancer | Square | Small | #4A90E2 | #000000 | 1pt |
| Security Appliance | Square | Small | #D0021B | #000000 | 1pt |
| Storage | Square | Small | #4A4A4A | #000000 | 1pt |
| External Network | Cloud | Large | #B8E986 | #000000 | 1pt |

Size Definition:
- Small = Base unit (X) = 80px
- Large = 2X = 160px

### Connection Standards

| Connection Type | Line Style | Color (Hex) | Width | Label Example (Optional) |
|----------------|------------|-------------|-------|--------------------------|
| Primary Path | Solid | #000000 | 1pt | Gi0/0 to Fa1/1         |
| Backup Path | Dashed | #4A90E2 | 1pt | Gi0/1 to Fa1/2         |
| VPN Tunnel | Dotted | #D0021B | 1pt | VPN-HQ-Branch          |
| Wireless Link  | Dashed-Dotted | #808080 | 1pt | SSID: CompanyWiFi       |
| Internet Connection | Solid | #FFA500 | 2pt | ISP: ExampleISP        |

## Layer 2 Standards

### VLAN Representation

#### VLAN Grouping
- Background: Light gray (#F5F5F5)
- Border: 1pt Solid #E0E0E0
- Label format:
  ```
  VLAN Name
  VLAN ID: xxx
  ```

#### VLAN Types
| Type | Notation | Example |
|------|----------|---------|
| Data VLAN | V[id] | V100 |
| Voice VLAN | VV[id] | VV200 |
| Native VLAN | VN[id] | VN1 |
| Private VLAN | VP[id] | VP300 |
| Management VLAN | VM[id] | VM10 |

### Port Types & Connections

#### Standard Port Types
| Type | Line Style | Width | Example Usage |
|------|------------|-------|---------------|
| Access | Solid | 1pt | End device connections |
| Trunk | Solid | 2pt | Switch interconnects |
| Channel | Double line | 2pt | Port aggregation |
| Monitor | Dashed | 1pt | SPAN/Mirror ports |

### VLAN Trunk Labeling

#### Inline Method (Primary Method for on-diagram clarity)
| Label Format | Meaning | Example |
|--------------|---------|---------|
| T[range] | Basic trunk | T100-200 |
| T* | All VLANs allowed | T* |
| T[vlan]N,[range] | Native VLAN specified | T10N,100-200 |
| TV[vlan],[range] | Voice VLAN specified | TV100,1-1000 |

#### Side Panel Method (For detailed documentation or when inline is too cluttered)
```
Link: [Device1] ↔ [Device2]
Status: Trunk
Allowed: [VLAN range]
Native: [VLAN]
Voice: [VLAN]
Mode: [Auto/On/Desirable]
Speed: [Speed]
```

### Spanning Tree Protocol

#### STP States
| State | Indicator | Text Color |
|-------|-----------|------------|
| Root Bridge | (R) | Black |
| Root Port | (RP) | Green |
| Designated | (D) | Black |
| Blocking | (B) | Red |
| Alternate | (A) | Blue |

#### Port Roles
| Role | Symbol | Usage |
|------|--------|--------|
| Edge Port | (E) | End device connections |
| P2P Link | (P) | Switch interconnects |
| Shared | (S) | Hub connections |
| Fast | (F) | Fast transition |

**Handling Multiple STP States:** In rare cases where a port might temporarily exhibit multiple STP states, prioritize the most significant state or use annotations for clarity.

### Link Aggregation

#### Protocol Indicators
| Symbol | Meaning |
|--------|----------|
| (LACP) | LACP Protocol |
| (PAgP) | PAgP Protocol |
| (Static) | Static configuration |

## Layer 3 Standards

### Text Contrast Rules
| Background Color | Text Color |
|-----------------|------------|
| Dark (#4A4A4A and darker) | White |
| Light (lighter than #4A4A4A) | Black |

### L3 Information Display

**Context:** Display L3 information when the diagram's focus is on routing, addressing, or network segmentation.

1. IP Addresses
   - Position: Below device name
   - Format: x.x.x.x/xx (CIDR notation)
   - Multiple IPs: Stack vertically
   - Font: Same as device labels (Arial/Helvetica 10pt)
   - Color: Based on contrast rules

2. Subnet Representation
   - Background: Light gray (#F5F5F5)
   - Border: 1pt Solid #E0E0E0
   - Label format:
     ```
     Network Name
     x.x.x.x/xx
     ```

3. Interface Labels
   - Size: 8pt Arial/Helvetica
   - Position: Near connection endpoint
   - Format: Standard interface naming (Gi0/0, etc.)
   - Color: Black
   - No background

**Routing Protocol Representation (Optional):** Indicate routing protocols using concise labels near relevant connections or within subnet representations (e.g., "OSPF," "BGP").

## Layout & Spacing

### Grid System
- Base unit: 80px (8 grid squares in draw.io)
- Vertical spacing: 160px between layers
- Horizontal spacing: 120px between peer elements
- Margin: 160px from page edge

**Flexibility for Large Diagrams:** While these guidelines are recommended, for very large and complex diagrams, prioritize logical grouping and readability, allowing for minor deviations as needed. Avoid overlapping elements and connection lines.

### Hierarchy
- Core infrastructure at center
- Distribution layer in middle
- Access layer at edges
- Flow direction: top-to-bottom or left-to-right (document any deviations and their rationale).

## Typography

### Standard Typography
All text elements use:
- Font: Arial or Helvetica
- Size: 10pt
- Color: Based on contrast rules
- Style: Regular
- Alignment: Left-aligned

Exception:
- Diagram Title: 14pt, Bold, Centered

## Tool-Specific Implementations

**General Advice for All Tools:**
- Utilize layers to organize elements and improve manageability.
- Group related objects to treat them as a single unit.
- Leverage style libraries or templates to maintain consistency.
- Export diagrams in standard formats like PDF or PNG for wider accessibility.

### draw.io Configuration
**How to Achieve Standards:**
1. Grid Setup:
   - Grid Size: 10px
   - Subdivisions: 1
   - View → Snap to Grid (enabled)
   - View → Grid (enabled)
2. Size Implementation:
   - Small elements: 80px (adjust width and height in the 'Properties' panel)
   - Large elements: 160px (adjust width and height in the 'Properties' panel)
   - Save commonly used shapes with predefined styles to a custom library for easy reuse.
3. Interactive Settings
```
// Common style string for network shapes
shape=rectangle;
pointer-events=1;
movable=1;
resizable=1;
rotatable=0;
deletable=1;
editable=1;
connectable=1;
```

### Visio Configuration
**How to Achieve Standards:**
- Base unit: 0.8 inches (configure in 'Design' -> 'Size' -> 'More Page Sizes')
- Enable Snap to Grid (View -> Visual Aids -> Snap to Grid)
- Set shape dimensions precisely using the 'Shape Format' pane.

### PowerPoint Configuration
**How to Achieve Standards:**
- Grid spacing: 0.8 inches (View -> Grid and Guides -> Grid Settings)
- Enable Snap objects to grid (View -> Grid and Guides -> Snap objects to grid)
- Size shapes numerically in the 'Shape Format' pane to maintain proportions.

## Documentation Requirements

### Metadata
- Diagram title
- Version number
- Author
- Last modified date
- Environment (prod/dev/test)
- Intended Audience
- Change Log/Revision History (Date, Version, Author, Description of Changes)
- Dependencies/Related Documents

### Required Technical Information
- IP addresses and subnets
- Interface names
- VLAN assignments
- Protocol information
- Security zones

## Best Practices
1. **Start with a Template:** Utilize pre-configured templates to ensure adherence to basic standards.
2. **Use Standard Sizes Consistently:** Avoid deviating from defined sizes unless absolutely necessary and clearly documented.
3. **Include Legend:** Provide a comprehensive legend explaining all shapes and connection types used in the diagram.
4. **Archive Versions:** Maintain an archive of previous diagram versions for auditing and historical reference.
5. **Review for Readability:** Ensure the diagram is easy to understand and free of clutter.
6. **Validate Against Standards:**  Before finalizing, review the diagram against this document's guidelines.
7. **Use Inline Labels for Quick Reference:**  Utilize inline labels for connections and devices to provide immediate context.
8. **Keep Consistent Spacing:** Maintain uniform spacing between elements for a clean and organized look.
9. **Show Primary Paths Clearly:** Emphasize primary network paths using solid lines and potentially thicker widths.
10. **Include Relevant Status Information:**  Where applicable, indicate the operational status of key components.
11. **Document Deviations:** If deviations from these standards are necessary, document the reasons clearly.

## Quality Control Checklist
- Standard shapes used
- Correct colors applied
- Specified border styles and widths used
- Grid spacing followed
- Typography consistent
- Legend includes all shapes and connection types
- Version documented in metadata
- All connections properly styled
- IP addressing and other technical details accurate
- Diagram reviewed for readability and clarity

## Accessibility
- **Maintain a 4.5:1 minimum contrast ratio:** Use online tools to verify color contrast.
- **Utilize patterns in addition to color:** For example, use different fill patterns for elements with the same color.
- **Provide alternative text descriptions for shapes:** This allows screen readers to convey the diagram's information.
- **Ensure consistent scaling:** Avoid elements that become illegible when zoomed in or out.

## Security Considerations
- **Exclude sensitive data when possible:** Avoid including highly confidential information directly in the diagram.
- **Mark classifications appropriately:** If the diagram contains sensitive information, label it according to your organization's data classification policy.
- **Create audience-appropriate versions:**  Develop different versions of the diagram with varying levels of detail for different audiences.
- **Control access to diagrams:** Store diagrams in secure locations with appropriate access controls.

