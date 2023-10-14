.PHONY: clean

.APP_NAME = soda
.APP_VERSION = 6.1.2
.BUILD_FLAGS = -trimpath

.DARWIN_AMD64_DIR = releases/$(.APP_VERSION)/darwin-amd64
.DARWIN_AMD64_ARCHIVE = $(.APP_NAME)_$(.APP_VERSION)_darwin_amd64.tar.gz
.DARWIN_ARM64_DIR = releases/$(.APP_VERSION)/darwin-arm64
.DARWIN_ARM64_ARCHIVE = $(.APP_NAME)_$(.APP_VERSION)_darwin_arm64.tar.gz
.LINUX_AMD64_DIR = releases/$(.APP_VERSION)/linux-amd64
.LINUX_AMD64_ARCHIVE = $(.APP_NAME)_$(.APP_VERSION)_linux_amd64.tar.gz
.WINDOWS_AMD64_DIR = releases/$(.APP_VERSION)/windows-amd64
.WINDOWS_AMD64_ARCHIVE = $(.APP_NAME)_$(.APP_VERSION)_windows_amd64.zip
.CHECKSUMS_TXT = releases/$(.APP_VERSION)/checksums.txt

build:
	go build -o builds/$(.APP_NAME) $(.BUILD_FLAGS)

clean:
	@rm -rf releases/$(.APP_VERSION)
	@echo "\033[32mMake clean finished.\033[0m"

release-darwin-amd64:
	@echo "\033[36mdarwin-amd64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf $(.DARWIN_AMD64_DIR)
	@mkdir -p $(.DARWIN_AMD64_DIR)

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build -o $(.DARWIN_AMD64_DIR)/$(.APP_NAME) $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@tar -zcf $(.DARWIN_AMD64_DIR)/$(.DARWIN_AMD64_ARCHIVE) -C $(.DARWIN_AMD64_DIR) $(.APP_NAME)

	@echo "\033[33mWriting to checksums.txt...\033[0m"
	@shasum -a 256 $(.DARWIN_AMD64_DIR)/$(.DARWIN_AMD64_ARCHIVE) | awk '{split($$2, a, /\//); printf "%s  %s\n", $$1, a[4]}' >> $(.CHECKSUMS_TXT)

	@echo "\033[32mMake release file finished.\033[0m"

release-darwin-arm64:
	@echo "\033[36mdarwin-arm64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf $(.DARWIN_ARM64_DIR)
	@mkdir -p $(.DARWIN_ARM64_DIR)

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=darwin GOARCH=arm64 go build -o $(.DARWIN_ARM64_DIR)/$(.APP_NAME) $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@tar -zcf $(.DARWIN_ARM64_DIR)/$(.DARWIN_ARM64_ARCHIVE) -C $(.DARWIN_ARM64_DIR) $(.APP_NAME)

	@echo "\033[33mWriting to checksums.txt...\033[0m"
	@shasum -a 256 $(.DARWIN_ARM64_DIR)/$(.DARWIN_ARM64_ARCHIVE) | awk '{split($$2, a, /\//); printf "%s  %s\n", $$1, a[4]}' >> $(.CHECKSUMS_TXT)

	@echo "\033[32mMake release file finished.\033[0m"

release-linux-amd64:
	@echo "\033[36mlinux-amd64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf $(.LINUX_AMD64_DIR)
	@mkdir -p $(.LINUX_AMD64_DIR)

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o $(.LINUX_AMD64_DIR)/$(.APP_NAME) $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@tar -zcf $(.LINUX_AMD64_DIR)/$(.LINUX_AMD64_ARCHIVE) -C $(.LINUX_AMD64_DIR) $(.APP_NAME)

	@echo "\033[33mWriting to checksums.txt...\033[0m"
	@shasum -a 256 $(.LINUX_AMD64_DIR)/$(.LINUX_AMD64_ARCHIVE) | awk '{split($$2, a, /\//); printf "%s  %s\n", $$1, a[4]}' >> $(.CHECKSUMS_TXT)

	@echo "\033[32mMake release file finished.\033[0m"

release-windows-amd64:
	@echo "\033[36mwindows-amd64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf $(.WINDOWS_AMD64_DIR)
	@mkdir -p $(.WINDOWS_AMD64_DIR)

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build -o $(.WINDOWS_AMD64_DIR)/$(.APP_NAME).exe $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@zip -r -j -q $(.WINDOWS_AMD64_DIR)/$(.WINDOWS_AMD64_ARCHIVE) $(.WINDOWS_AMD64_DIR)/$(.APP_NAME).exe

	@echo "\033[33mWriting to checksums.txt...\033[0m"
	@shasum -a 256 $(.WINDOWS_AMD64_DIR)/$(.WINDOWS_AMD64_ARCHIVE) | awk '{split($$2, a, /\//); printf "%s  %s", $$1, a[4]}' >> $(.CHECKSUMS_TXT)

	@echo "\033[32mMake release file finished.\033[0m"

# release-all: clean release-darwin-amd64 release-darwin-arm64 release-linux-amd64 release-windows-amd64
release-all:
	@$(MAKE) clean
	@echo
	@$(MAKE) release-darwin-amd64
	@echo
	@$(MAKE) release-darwin-arm64
	@echo
	@$(MAKE) release-linux-amd64
	@echo
	@$(MAKE) release-windows-amd64
