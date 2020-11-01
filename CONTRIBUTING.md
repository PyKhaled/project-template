# Contributing

When contributing to this repository, please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change. 

Please note we have a code of conduct, please follow it in all your interactions with the project.

## Contributing a new project template

If you'd like to contribute a new built-in project template to be distributed with GitLab, please do the following:

1. Create a new public project with the project content you'd like to contribute in a namespace of your choosing. You can view a working example [here](https://gitlab.com/gitlab-org/project-templates/dotnetcore).
   * Projects should be as simple as possible and free of any unnecessary assets or dependencies.
1. When the project is ready for review, please create a new issue in [gitlab-ce](https://gitlab.com/gitlab-org/gitlab/issues) with a link to your project.
   * In your issue, `@` mention the relevant Backend Engineering Manager and Product Manager for the [Templates category](https://about.gitlab.com/handbook/product/categories/#import-group).

To make the project template available when creating a new project, the vendoring process will have to be completed: 

1. Create a working template ([example](https://gitlab.com/gitlab-org/project-templates/dotnetcore))
1. Add boilerplate to
    - `gitlab/lib/gitlab/project_template.rb`,
    - `gitlab/spec/lib/gitlab/project_template.rb`, and
    - `gitlab/app/assets/javascripts/projects/project_new.js`.

    See MR [!25486](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/25486) for an example
1. Run the following in the `gitlab` project, where `$name` is the name you gave the template in `gitlab/lib/gitlab/project_template.rb`
   ```bash
   bin/rake gitlab:update_project_templates[$name]
   ```
1. Run the [bundle_repo](/bundle_repo) script
1. Add exported project (`$name.tar.gz`) to `gitlab/vendor/project_templates` and remove the resulting build folders `tar-base` and `project`
1. Run `bin/rake gettext:regenerate` in the `gitlab` project and commit new `.pot` file
1. Add changelog (e.g. `bin/changelog -m 25486 "Add Project template for .NET"`)
1. Add icon to https://gitlab.com/gitlab-org/gitlab-svgs, as show in [this example](https://gitlab.com/gitlab-org/gitlab-svgs/merge_requests/195)
1. Run `yarn run svgs` on `gitlab-svgs` project and commit result
1. Forward changes in `gitlab-svgs` project to master
1. Rebase master to pick up new svgs
1. Test everything is working

## Contributing an improvement to an existing template

Existing templates are available in the [project-templates](https://gitlab.com/gitlab-org/project-templates)
group.

To contribute a change, please open a merge request in the relevant project
and mention @jeremy when you are ready for a review.

Then, if your merge request gets accepted, either open an issue on
`gitlab` to ask for it to get updated, or open a merge request updating
the vendored template using the command

```bash
bin/rake gitlab:update_project_templates[$name]
```

as above, where `$name` is the name of the template that you want to be updated.


## Commit Messages

### Message Structure

A commit messages consists of three distinct parts separated by a blank line: the title, an optional body and an optional footer. The layout looks like this:

```
type: subject

body

footer
The title consists of the type of the message and subject.
```


### The Type

The type is contained within the title and can be one of these types:

* feat: a new feature
* fix: a bug fix
* docs: changes to documentation
* style: formatting, missing semi colons, etc; no code change
* refactor: refactoring production code
* test: adding tests, refactoring test; no production code change
* chore: updating build tasks, package manager configs, etc; no production code change


### The Subject

Subjects should be no greater than 50 characters, should begin with a capital letter and do not end with a period.

Use an imperative tone to describe what a commit does, rather than what it did. For example, use change; not changed or changes.

### The Body

Not all commits are complex enough to warrant a body, therefore it is optional and only used when a commit requires a bit of explanation and context. Use the body to explain the what and why of a commit, not the how.

When writing a body, the blank line between the title and the body is required and you should limit the length of each line to no more than 72 characters.

### The Footer
The footer is optional and is used to reference issue tracker IDs.

### Example Commit Message

```plain
feat: Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

## Pull Request Process

1. Ensure any install or build dependencies are removed before the end of the layer when doing a 
   build.
2. Update the README.md with details of changes to the interface, this includes new environment 
   variables, exposed ports, useful file locations and container parameters.
3. Increase the version numbers in any examples files and the README.md to the new version that this
   Pull Request would represent. The versioning scheme we use is [SemVer](http://semver.org/).
4. You may merge the Pull Request in once you have the sign-off of two other developers, or if you 
   do not have permission to do that, you may request the second reviewer to merge it for you.

