# Development

## Environment

OPA is written in the [Go](https://golang.org) programming language.

If you are not familiar with Go we recommend you read through the [How to Write Go
Code](https://golang.org/doc/code.html) article to familiarize yourself with the standard Go development environment.

Requirements:

- Git
- GitHub account (if you are contributing)
- Go (version 1.5.x and 1.6.x are supported)
- GNU Make

## Getting Started

After cloning the repository, you can run `make all` to build the project and
execute all of the tests. If this succeeds, there should be a binary
in the top directory (opa).

Verify the build was successful by running `opa version`.

You can re-build the project with `make build` and execute all of the tests
with `make test`.

## Workflow

1. Go to [https://github.com/open-policy-agent/opa](https://github.com/open-policy-agent/opa) and fork the repository
   into your account by clicking the "Fork" button.

1. Clone the fork to your local machine.

    ```
    cd $GOPATH
    mkdir -p src/github.com/open-policy-agent
    cd src/github.com/open-policy-agent
    git clone git@github.com/<GITHUB USERNAME>/opa.git opa
    cd opa
    git remote add upstream https://github.com/open-policy-agent/opa.git
    ```

1. Create a branch for your changes.

    ```
    git checkout -b somefeature
    ```

1. Update your local branch with upstream.

    ```
    git fetch upstream
    git rebase upstream/master
    ```

1. Develop your changes and regularly update your local branch against upstream.

	- Make sure you run `go fmt` on your code before submitting a Pull Request.

1. Commit changes and push to your fork.

    ```
    git commit
    git push origin somefeature
    ```

1. Submit a Pull Request via https://github.com/\<GITHUB USERNAME>/opa. You
   should be prompted to with a "Compare and Pull Request" button that
   mentions your branch.

1. Once your Pull Request has been reviewed and signed off please squash your
   commits. If you have a specific reason to leave multiple commits in the
   Pull Request, please mention it in the discussion.

   > If you are not familiar with squashing commits, see [the following blog post for a good overview](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html).

## Dependencies

[Glide](https://github.com/Masterminds/glide) is a command line tool used for
dependency management. You must have Glide installed in order to add new
dependencies or update existing dependencies. If you are not changing
dependencies you do not have to install Glide, all of the dependencies are
contained in the vendor directory.

If you need to add a dependency to the project:

1. Run `glide get <package>` to download the package.
    - This command should be used instead of `go get <package>`.
	- The package will be stored under the vendor directory.
	- The glide.yaml file will be updated.
1. Manually remove the VCS directories (e.g., .git, .hg, etc.) from the new
   vendor directories.
1. Commit the changes in glide.yaml, glide.lock, and new vendor directories.

If you need to update the dependencies:

1. Run `glide update --update-vendored`.
1. Commit the changes to the glide.lock file and any files under the vendor
   directory.

## Opalog

If you need to modify the Opalog syntax you must update opalog/parser.peg
and run `make generate` to re-generate the parser code.

> If you encounter an error because "pigeon" is not installed, run `glide
> rebuild` to build and install the vendored dependencies (which include the
> parser generator). Note, you will need to have [Glide](https://github.com/Masterminds/glide)
> installed for this.

Commit the changes to the parser.peg and parser.go files.