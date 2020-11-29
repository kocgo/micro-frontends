## Definition of tech stack for each part of the application

## Definition of requirements:

#### Inflexible Requirement 1
- No shared context between child projects (state, imports etc)
- Shared modules through Modules Federation are okay

#### Inflexible Requirement 2
- Container should not assume that a child is using a particular framework
- Communication should be done with callbacks or events.
