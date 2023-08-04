# Membership

**Note:** This document is a work in progress

This doc outlines the various responsibilities of contributor roles in Universal Blue.

This document is derived from [Kubernetes](https://github.com/kubernetes/community/blob/master/community-membership.md). 

## New contributors

New contributors should be welcomed to the community by existing members,
helped with PR workflow, and directed to relevant documentation and
communication channels. 

This informal level is designed for drive-by contributors or those who might be 
interested in participating in open source and using this project to learn how.

We encourage anyone to participate, and for those who wish to earn more responsibilities 
and begin their open source journey with us ... apply within. Vegeta tests us all. 

## Members and Approvers

Established community members are expected to demonstrate their adherence to the
principles in this document, familiarity with project organization, roles,
policies, procedures, conventions, etc., and technical and/or writing ability.
Role-specific expectations, responsibilities, and requirements are enumerated
below.
 
### Member

Members are *[continuously active]* contributors in the community. They can have
issues and PRs assigned to them, and participate in GitHub teams. Members are expected to
remain active contributors to the community. This role includes responsiblities 
that are defined as "Reviewers" in other cloud native projects. 

**Defined by:** Inclusion in the Member team in the Universal Blue GitHub organization

- Enabled two-factor authentication on their GitHub account
- Have made **multiple contributions** to the project or community, enough to
  demonstrate an **ongoing and long-term commitment** to the project.
  Contributions may include, but is not limited to:
    - Authoring or reviewing PRs on GitHub, with at least one **merged** PR.
      **NOTE:** The PR(s) must demonstrate an ongoing and active commitment.
      A few examples include:
      - A single issue/PR that has taken several weeks of driving consensus
      - A larger number of smaller PRs over several weeks to months
      - A smaller number of complex or technical PRs that required working with
        community members to resolve an issue (e.g. regressions, bugs fixes etc)
    - Filing or commenting on issues on GitHub
    - Contributing to community discussions
    - Special consideration of established open source contributions
      - Distribution maintainer, CNCF Contributor, Apache,  etc.
      - This one means a lot - it's the life blood.    
- Have read the contributor guide
- Actively contributing to 1 or more repositories.
- Sponsored by 2 Approvers. **Note the following requirements for sponsors**:
    - Sponsors must have close interactions with the prospective member - e.g. code/design/proposal review, coordinating
      on issues, etc.
    - Sponsors must be reviewers or approvers in at least one repo in the organization.
- **[Open an issue][membership request] against the ublue-os/main repo**
   - Ensure your sponsors are @mentioned on the issue
   - Complete every item on the checklist
   - Make sure that the list of contributions included is representative of your work on the project.
- Have your sponsoring reviewers reply confirmation of sponsorship: `+1`
- Once your sponsors have responded, your request will be reviewed by the Owners and acted upon. You have ascended.

#### Responsibilities and privileges

- Proactively act when builds are failing
  - Internal project outages should be prioritized over external dependencies
  - If outage is complex ensure that the rest of the team is aware of your work by filing an issue
- Responsive to issues and PRs assigned to them
- Responsive to mentions of teams they are members of
- Active owner of code they have contributed (unless ownership is explicitly transferred)
  - Code is well tested
  - Keeps the tree green
  - Addresses bugs or issues discovered after code is accepted
- They can be assigned to issues and PRs, and people can ask members for reviews with a `/cc @username`.

**Note:** Members who frequently contribute code are expected to proactively
perform code reviews and work towards becoming a primary *approver* for the
reopository that they are active in.

### Approver

Code approvers are able to both review and approve code contributions.  While
code review is focused on code quality and correctness, approval is focused on
holistic acceptance of a contribution including: backwards / forwards
compatibility, subtle performance and correctness issues, alignment with upstream 
features and plans, and in general are the drivers of the project.  

**Defined by:** Inclusion in the Approver team in the Universal Blue GitHub organization

#### Requirements

- Member for at least 3 months
- Primary reviewer for at least 5 PRs to the codebase
- Reviewed or merged at least 20 substantial PRs to the codebase 
- Demonstrate sound technical judgement
- Responsible for project quality control via code reviews
  - With a focus on long term sustainability to the project
- Expected to be responsive to review requests as per [community expectations]
- Mentor new contributors and members
- Deep understanding of our working relationship with Fedora and other upstreams
  - Is invested in keeping track of upstream issues that affect our repositories
  - Is comfortable reporting and testing issues upstream
  
#### Responsibilities and privileges

- Approver status may be a precondition to accepting large code contributions
- Demonstrate sound technical judgement
  - Is actively monitoring upstream projects and participating accordingly as good open source citizens.
  - This may include rejecting ideas in order to maintain project scope
- Responsible for project quality control via code reviews
- Expected to be responsive to review requests as per [community expectations]
- Mentor new contributors and reviewers

## Inactive members

_Members are continuously active contributors in the community._

A core principle in maintaining a healthy community is encouraging active
participation. It is inevitable that people's focuses will change over time and
they are not expected to be actively contributing forever.

However, being a member of one of the Universal Blue GitHub organizations comes with
an elevated set of permissions. These capabilities should not be used by those
that are not familiar with the current state of the Kubernetes project.

Therefore members with an extended period away from the project with no activity
will be removed from the Universal Blue GitHub Organizations and will be required to
go through the org membership process again after re-familiarizing themselves
with the current state.

### How inactivity is measured

Inactive members are defined as members of one of the Universal Blue Organizations
with **no** contributions across any organization over the past 6 months. This is
measured by GitHub activity.

After an extended period away from the project with no activity
those members would need to re-familiarize themselves with the current state
before being able to contribute effectively.


## Owner

Jorge Castro (@castrojo) and Marco Ceppi (@ceppimarco) are in the owner group for a few reasons.

- Administrative things like billing info, and later on taxes and stuff.
- Distributed ownership is hard thing for a small open source project
  - Therefor are codified as as adminstrative owners
  - Are just Approvers that get stuck with the cloud bill


[contributor guide]: /contributors/guide/README.md
