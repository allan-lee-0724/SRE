# Incident Management
- The goal of an SRE is to MANAGE incidents as they happen 
- An incident is a serious occurence as defined by either your company, stakeholders, or users
    - Company: can't access internal tools used to do job
    - Stakeholders: a service is down that will hurt company relationships with the public
    - Users: unable to access service, unexpected results, etc

There are some general guidelines when determining if an issue constitutes an incident or not:
- Is the problem user facing?
- Are multiple teams/departments needed to solve the issue?
- Is it taking too long to solve the issue?
- Is a manual response required?
- Did monitoring tools/alerts not alert you to the issue?
- Was any data lost?
- Was user data exposed?

## Incident Management Guiding Properties
- Maintain clear line of command
- Designate clearly defined roles
- Keep records of debugging/mitigation solutions
- Declare incidents sooner rather than later

## Incident Command System
Firefighters developed the Incident Command System in 1968 to better manage dealing with forest fires. There are
three guiding principles for ICS that work well with the incident management guiding principles
- Coordinate
- Communicate
- Control

When managing an incident there are three primary leadership roles that should be filled by individuals who can 
consistently maintain an environment of control, communication, and coordination:
- Incident Commander
    - If you declare an incident, you start as the incident commander
        - You can hand off this responsibility later if necessary, but you will start in this role
    - You are the coordinator between teams
    - You delegate responsibilities
        - When an incident starts, you assume the Communications Lead and Ops Lead positions until you can 
        delegate them
- Communications Lead
    - You handle communication with those outside of the incident management team
    - Any pertinent information is given to the Incident Commander who can then share it with the appropriate
    teams
- Ops Lead
    - You handle the team that is working to solve the issue
        - This can be someone from SRE, or Dev, or another team. Once the source of the issue is found you might
        want to switch who is the Ops Lead depending on the issue
    - They can roll back a deployment
    - They can redirect traffic from a corrupt node to another one
    - They can raise computing power for a virtual machine
    - etc

# Postmortem
A Postmortem is a document that provides context for an incident after the fact. It should include as much detail
about the incident as can be provided reasonably: 
- When did the incident happen?
- Who worked on the incident to solve it?
- What was the incident (basic summary of incident)?
- What happend (more detailed explanation)
- Timeline of events
- Mitigation efforts taken
- Damage done
- Solution to incident
- Recovery efforts
- etc

## Postmortem: Blameless culture
It can be very easy to think that your mistakes are yours alone and that you will be blamed/get in trouble for
making a mistake: this kind of thinking can lead to incomplete Postmortem reports that don't actually help anyone 
deal with the same issue in the future. To avoid this, a Blameless culture should be encouraged surrounding
Postmortem reports. 
- Blameless incident summary:
    - At 12:32 PM on December 25th, 2022 a corrupt image was deployed to the production environment instead of the
    newly corrected one. Due to this, a memory leak spiraled our of control which lead to VMs crashing, rebooting,
    and the process repeating. After 2 hours of searching the logs and system metrics the typo was discovered in
    the deployment configuration, changed, and the system began to work as expected.
- Blameful incident summary:
    - Eric was at it again this weekend: he made a typo in the deployment configuration which caused the entire
    SRE and development team to miss out on Christmas with their families. After the other SREs and Dev team
    members (not Eric, he was crying in the corner) exhausted the logs and system metrics, Sally, the hero of the
    day (unlike Eric, remember, he made us all miss Christmas) realized that Eric made a typo in the deployment
    configuration, and then we forced him to fix it while we all stared at him

There should be collaboration while creating the document, because not everyone has the whole picture. Also, 
senior members of the teams involved should review the document before it is approved in order to ensure the
document is sufficient
