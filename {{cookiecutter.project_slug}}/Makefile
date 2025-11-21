NAME := {{cookiecutter.project_slug}}
CRATE_NAME := {{cookiecutter.crate_name}}

all: copr-build srpm sources rust2rpm create-copr-repo

.PHONY: create-copr-repo
create-copr-repo:
	copr create rust-$(NAME) \
		{% for chroot in cookiecutter.chroots %}
		--chroot {{chroot}} \
		{% endfor %}
		--packit-forge-project-allowed github.com/r0x0d/{{cookiecutter.project_slug}}

.PHONY: create-gh-repo
create-gh-repo:
	gh repo create {{cookiecutter.project_slug}} \
		--public \
		--disable-wiki \
		--remote origin \
		--description "Upstream rpm repository for {{cookiecutter.upstream_repo_name}}" 

.PHONY: rust2rpm
rust2rpm:
	rust2rpm $(CRATE_NAME)

.PHONY: sources
sources:
	spectool -g $(NAME).spec

.PHONY: srpm
srpm:
	fedpkg srpm

.PHONY: copr-build
copr-build:
	copr build $(NAME) $(NAME)*.src.rpm
