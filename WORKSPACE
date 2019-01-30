load(
    "@bazel_tools//tools/build_defs/repo:http.bzl",
    "http_archive",
    "http_file",
)

# Additional bazel rules
http_archive(
    name = "io_bazel_rules_go",
    url = "https://github.com/bazelbuild/rules_go/releases/download/0.16.5/rules_go-0.16.5.tar.gz",
    sha256 = "7be7dc01f1e0afdba6c8eb2b43d2fa01c743be1b9273ab1eaf6c233df078d705",
)

http_archive(
    name = "bazel_gazelle",
    urls = ["https://github.com/bazelbuild/bazel-gazelle/releases/download/0.16.0/bazel-gazelle-0.16.0.tar.gz"],
    sha256 = "7949fc6cc17b5b191103e97481cf8889217263acf52e00b560683413af204fcb",
)

load(
    "@bazel_tools//tools/build_defs/repo:git.bzl",
    "git_repository",
)

git_repository(
    name = "io_bazel_rules_docker",
    remote = "https://github.com/bazelbuild/rules_docker.git",
    tag = "v0.5.1",
)

# Libvirt dependencies
http_file(
    name = "libvirt_libs",
    urls = [
        "https://libvirt.org/sources/libvirt-libs-5.0.0-1.fc28.x86_64.rpm",
    ],
    sha256 = "95d317fd645fb52745d642578263a9bcb0d796beadf00aeadebc0d692f5529ba",
)

http_file(
    name = "libvirt_devel",
    urls = [
        "https://libvirt.org/sources/libvirt-devel-5.0.0-1.fc28.x86_64.rpm",
    ],
    sha256 = "6573a047d777ed00f6858c2e75c780053b1f898ae1c3f7415e991c94c5ccdd70",
)

# Disk images
http_file(
    name = "alpine_image",
    urls = [
        "http://dl-cdn.alpinelinux.org/alpine/v3.7/releases/x86_64/alpine-virt-3.7.0-x86_64.iso",
    ],
    sha256 = "5a4b2588afd32e7024dd61d9558b77b03a4f3189cb4c9fc05e9e944fb780acdd",
)

http_file(
    name = "cirros_image",
    urls = [
        "https://download.cirros-cloud.net/0.4.0/cirros-0.4.0-x86_64-disk.img",
    ],
    sha256 = "a8dd75ecffd4cdd96072d60c2237b448e0c8b2bc94d57f10fdbc8c481d9005b8",
)

http_file(
    name = "fedora_image",
    urls = [
        "https://download.fedoraproject.org/pub/fedora/linux/releases/29/Cloud/x86_64/images/Fedora-Cloud-Base-29-1.2.x86_64.qcow2",
    ],
    sha256 = "a30549d620bf6bf41d30a9a58626e59dfa70bb011fd7d50f6c4511ad2e479a39",
)

http_file(
    name = "virtio_win_image",
    urls = [
        "https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso",
    ],
    sha256 = "43c969f99b02ec6467ecb1f6d93689327a248cfa8de9c4b34d65b6b41e7bc556",
)

load(
    "@io_bazel_rules_go//go:def.bzl",
    "go_rules_dependencies",
    "go_register_toolchains",
)
go_rules_dependencies()
go_register_toolchains()

load(
    "@bazel_gazelle//:deps.bzl",
    "gazelle_dependencies",
    "go_repository",
)
gazelle_dependencies()

# Winrmcli dependencies
go_repository(
    name = "com_github_masterzen_winrmcli",
    commit = "c85a68ee8b6e3ac95af2a5fd62d2f41c9e9c5f32",
    importpath = "github.com/masterzen/winrm-cli",
)

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
    "container_image",
    container_repositories = "repositories",
)
container_repositories()

# Pull base image fedora28
container_pull(
  name = "fedora",
  registry = "index.docker.io",
  repository = "library/fedora",
  digest = "sha256:57d86e03971841e79585379f8346289ceb5a3e8ee06933fbd5064b4f004659d1",
  #tag = "28",
)

# Pull base image libvirt
container_pull(
  name = "libvirt",
  registry = "index.docker.io",
  repository = "alukiano/libvirt",
  digest = "sha256:23cb9e64909fb9519d1b256ceefc546deb3eb81ccbe7e83c3ef461a7cd2b3da9",
  #tag = "4.9.0",
)

# Pull base image cdi-http-import-server
container_pull(
  name = "cdi-http-import-server-base",
  registry = "index.docker.io",
  repository = "kubevirt/cdi-http-import-server-base",
  digest = "sha256:7cf1dd568d853884e558f714a24566682c091ff783495cccac0349e82c8a874f",
  #tag = "28",
)

load(
    "@io_bazel_rules_docker//go:image.bzl",
    _go_image_repos = "repositories",
)
_go_image_repos()
