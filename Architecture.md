## Definition of tech stack for each project

## Definition of requirements

#### Inflexible Requirement 1
- No shared context between child projects (state, imports etc)
- Shared modules through Modules Federation are okay

#### Inflexible Requirement 2
- Container should not assume that a child is using a particular framework
- Frameworks may become obsolete
- Communication should be done with callbacks or events.

#### Inflexible Requirement 3
- Styling from one project should never affect another

#### Inflexible Requirement 4
- Version control should not have any impact (monorepo or seperate)

#### Inflexible Requirement 5
- Container project should be able to use any version of the child projects.

