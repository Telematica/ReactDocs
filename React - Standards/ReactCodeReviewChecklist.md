# React - Code Review Checklist

*When performing a code review on a react story here are some helpful guidelines to know what to look out for:*

### Style
* Make sure it matches the mockups.
* Check that it is first styling with the theme, then JSS where theme doesn't work and avoiding inline styling.
* Make sure there aren't any repeating styles in multiple files.

### Component
* Make sure there are unit tests and that the test coverage for that component is at least 90%.
* Make sure the folder structure and naming conventions match our guidelines: [Folder Structure for React Projects](https://dealersocket.atlassian.net/wiki/spaces/TRIBEINVENTORY/pages/671548067/Folder+Structure+for+React+Projects).
* Make sure that it is using e2e tags where necessary: [Data e2e Attributes in React Projects](https://dealersocket.atlassian.net/wiki/spaces/TRIBEINVENTORY/pages/671417081/Data+e2e+Attributes+in+React+Projects).


## __Storybook__

* Ensure your component is added to the storybook.
* Ensure you have notes relevant to the component.
* Add knobs and actions where ever necessary to the component.
* Ensure you have all the scenarios covered for your component in the storybook. For example "Basic", "Advanced" or any relevant naming for your component.

### App.Settings

* Ensure communication of App.Settings changes are properly communicated to your respective Tribes

### Code Review
* Ensure you get approval from at least 3 engineers. 
* Remember to remind reviewers of changes made. Reviewers are responsible for code as well and may not be actively monitoring a particular pull request.
* Add screenshots to show before and after to speed up the approval process