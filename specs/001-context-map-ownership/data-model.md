# Data Model

## Entities

- **Layer**
  - Fields: id, name, purpose, scope, owner (team/role), contact path, engagement rules/SLAs, last_updated, friction_status (low/attention/unknown)
  - Relationships: has many Components/Services
  - Validation: name unique; owner/contact required

- **Component/Service**
  - Fields: id, layer_id, name, description, owner (team/role), contact path, dependencies (list of Dependency refs), friction_indicators (list), last_updated
  - Relationships: belongs to Layer; has many Dependencies (as source/target)
  - Validation: name unique within layer; owner/contact required; dependencies reference valid components

- **Owner**
  - Fields: id, team_name, role, contact (mail/Slack/form), engagement_rules, SLA cues
  - Relationships: associated with Layers and Components
  - Validation: contact required; engagement_rules present

- **Dependency/Interaction**
  - Fields: id, source_component, target_component, expectation/SLA, notes
  - Relationships: links Components (source → target)
  - Validation: source/target must exist; expectation required

- **Friction Indicator**
  - Fields: id, component_ref, description, severity (info/warn/critical), status (open/in-progress/resolved), owner
  - Relationships: attached to Component/Service and Owner
  - Validation: severity required; owner required

- **Executive Summary**
  - Fields: ownership_clarity (high/medium/low), key_dependencies (list of IDs), top_friction (list of indicators), last_updated, contact_for_updates
  - Relationships: references Layers, Components, Friction Indicators
  - Validation: ownership_clarity required; last_updated required
