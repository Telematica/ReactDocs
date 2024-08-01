# Definition of Done

__A Definition of Done (DoD)__ ensures a shared understanding within the team of what it means for work to be complete. The Definition of Done may vary depending on the specifics of the project, but the goal is to ensure that when a task, user story, or feature is labeled as "done," ittruly is finished to a quality standard, ready for delivery, and does not need any further work.

## Why DoD?

- __Ensures Quality and Consistency__: By establishing clear, comprehensive criteria that must be met before a task or feature can be considered "done", the Definition of Done (DoD) __ensures that the team consistently produces high-quality work__. It helps prevent the delivery of substandard or incomplete work, enhancing the final product's value and customer satisfaction.

- __Boosts Efficiency and Predictability__: The DoD __reduces the likelihood of rework__ and revisiting completed tasks, as it __ensures that all necessary elements of a task are addressed__ the first time around. It also __improves the predictability__ of the team's progress and the time it takes to complete tasks, making it easier to plan and manage the project timeline.

- __Promotes Transparency and Shared Understanding__: The DoD promotes a __shared understanding__ among the team of what it means for work to be complete. This enhances transparency, facilitates better communication, and reduces miscommunication or misunderstandings about the status of tasks, thereby improving teamwork and project outcomes. 

## How to Use DoD Checklist?

The DoD checklist is organized into four key categories: Quality Assurance and Testing, Design and Development Standards, Release and Deployment Management and Risk and Compliance Management. By diligently applying this checklist, teams can ensure projectsnot only meet but exceed expectations.

Here are 8 steps to leverage the DoD Checklist:

1. __Familiarize with the Checklist:__ Begin by thoroughly understanding each item on the DoD Checklist and ensure all team members are aware of these criteria. If you have questions or feedback, reach out via Slack #dod_questions. 

2. __Integrate into Project Lifecycle:__ Incorporate the checklist items into different stages of your project lifecycle. For instance, integrate quality assurance and testing steps during the development phase, and focus on release and deployment management as you approach project completion.

3. __Regular Reviews and Updates:__ Conduct regular reviews of the checklist items throughout the project. This ensures ongoing compliance and allows for timely adjustments in response to project evolution or unforeseen challenges.

4. __Collaborative Approach:__ Encourage collaboration among different teams –development, design, quality assurance, and operations –to address each checklist item. This promotes a holistic approach to project completion and ensures diverse perspectives are considered.

5. __Stakeholder Engagement:__ Engage stakeholders at various stages of the project, especially for sign-offs and feedback. This ensures alignment with broader business goals and stakeholder expectations.

6. __Documentation and Record Keeping:__ Encourage documentation of completed checklists items in Jira tickets. This not only provides a clear record of compliance but also provides support for root cause analysis or audits.

7. __Risk Management:__ Don’t forget to consider the risk and compliance management items on the checklist. Addressing these proactively helps in mitigating potential legal, cybersecurity, and operational risks.

8. __Continuous Improvement:__ Use the checklist as a tool for continuous improvement. Post-project reviews focusing on the checklist can reveal insights for enhancing processes and updating the checklist itself.

## DoD Checklist

### Quality Assurance and Testing

- __Code Reviewed:__ The __code has been reviewed__ by at least one other team member and __meets our coding quality standards__. All code has proper documentation and has been committed to the version control system.

- __Defect Management:__ __No P0 or P1 bugs__ (high-priority/consumer,customerorgrowthcritical paths) are open __prior to launch__. Any bugs that are found after release are addressed in accordance with Production Defect SLA’s. All high-priority bugs have been addressed, tested, and closed, ensuring the stability and reliability of the feature, user story, or task.

- __Testing: Meaningful automated integration tests, and system tests have been written__ and passed successfully.The code does not introduce any new bugs into our critical paths (consumer/customer/growth).

- __Browser Testing:__ Browser tests are conducted and pass successfully, ensuring compatibility and functionality across supported browsers and devices. Browser Testing Standard

- __Unit Test Coverage:__ Unit tests are reported in SonarQube and overall code coverage is 80% or more.

- __Analytics Testing:__ Analytics implementations have been tested usingTracking Validation Automation(TVA).  TVA ensures clickstream events adhere to event taxonomy standards and help with clickstream data accuracy and reliability.

- __Non-Functional Requirements:__ The feature, user story, or task meets any relevant non-functional requirements, such as performance, security, and usability.

- __Accessibility:__ The feature, user story, or task has been __[tested for accessibility](https://wave.webaim.org/extension/)__, and all necessary steps have been taken to address any newaccessibility issues. For assistance or questions: #a11y-best-practicesor#design-systems.

- __Integration:__ The code __integrates correctly__ into the existing system __without causing any disruption__ or negative impacts.


### Design and Development Standards

- __Product Design Reviewed:__ The feature, user story, or task aligns with the design spec and has been __reviewed AND approved by at least one member of the Product Design team__ (follow these guidelines: [Jira: Working with Design]()). This step includes a visual and usability review.

- __Alignment with Component System:__ The task, feature, or user story is in alignment with the correct component system for the build, using either the consumer-facing Haven [Design System’s]() [RDC-UI Component library]() or the customer-facing Harmony Design System’s Component Library (still in progress). For assistance or questions: #design-systems.

- __Alignment with Design and Tech Paved Paths:__ The task, feature, or user story aligns with our established Design and Tech Paved Paths, which outline our preferred technologies, architectures, and design principles.

- __Functionality:__ The feature, user story, or task fulfills all of its functional requirements and meets defined acceptance criteria as specified. It behaves as expected under all relevant conditions and inputs.


### Release and Deployment Management

- __Stakeholder Sign-Off:__ All relevant stakeholders have reviewed the task, feature, or user story and have provided their approval. This includes stakeholders from the business, technical, and user communities. Any feedback or change requests from these stakeholders have been adequately addressed, ensuring that the completed work aligns with stakeholder expectations and requirements.

- __Pre-Release Communication Plan:__ Develop a communication strategy before the release to inform all stakeholders and informed parties about the upcoming launch. This could include details like the release date, the features or updates included in the release, and any potential impacts orrequired actions on their part.

- __Success Measurement:__ Metrics to monitor and track the success of the new functionality have been identifiedand are in place to be tracked post-deployment. This could include factors like user adoption rates, reduction in manual processes, system performance improvements, etc. These metrics will allow us to evaluate the impact of the new feature, user story, or task and ensure it meets its intended objectives.

- __Core Web Vitals Monitoring:__ Teams have a plan in place to monitor their respective CWV Dashboard for 2 hours post release to ensure no degradation. Further details on steps to monitor CWV, point of contacts and SLA commitments can be found on [How to act on Core Web Vital (CWV) Alerts?]()

- __Documentation:__ We have documented test plansand release plans, and utilize these tools to minimize risk of negative user impact.

- __Deployment:__ The code has been successfully deployed into the staging environment, and, where necessary, the production environment.

### Risk and Compliance Management

- __Cybersecurity Risks:__ Our technical solutiondoes not increase our cybersecurity risk profile, with all necessary precautions taken to safeguard our system and data. Any identified cybersecurity risks have been addressed before the task or feature is considered "done."

- __Legal Risks:__ The solution has not introduced unexpected legal risks, including those related to open source licensing, data privacy, or intellectual property. Any such risks that have been identified are addressed and mitigated, ensuring our compliance with legal requirements and obligations before considering the task orfeature as "done."

- __Disaster Recovery Plan:__ Ensure there is a plan in place in case of a critical issue, such as a major bug or a security breach. This plan should include steps to mitigate the issue, protect user data, and restore normal operations as quickly as possible.
