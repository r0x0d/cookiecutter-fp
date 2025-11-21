NAME := {{cookiecutter.project_slug}}

all: copr-build srpm sources rust2rpm create-copr-repo

.PHONY: create-copr-repo
create-copr-repo:
	copr create rust-$(NAME) \
		--chroot {{cookiecutter.chroots}} \
		--packit-forge-project-allowed github.com/r0x0d/{{cookiecutter.project_slug}}

.PHONY: create-gh-repo
create-gh-repo:
	gh repo create {{cookiecutter.project_slug}} \
		--public \
		--disable-wiki \
		--description "Upstream rpm repository for {{cookiecutter.upstream_repo_name}}" 

.PHONY: rust2rpm
rust2rpm:
	rust2rpm $(NAME)

.PHONY: sources
sources:
	spectool -g rust-$(NAME).spec

.PHONY: srpm
srpm:
	fedpkg srpm

.PHONY: copr-build
copr-build:
	copr build $(NAME) rust-$(NAME)*.src.rpm
