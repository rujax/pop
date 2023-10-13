.APP_NAME = soda
.APP_VERSION = 6.1.2
.BUILD_FLAGS = -trimpath

build:
	go build $(.BUILD_FLAGS) .

release-darwin-amd64:
	@echo "\033[36mdarwin-amd64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf releases/darwin-amd64
	@mkdir -p releases/darwin-amd64

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build -o releases/darwin-amd64/$(.APP_NAME) $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@tar -zcf releases/darwin-amd64/$(.APP_NAME)_$(.APP_VERSION)_darwin_amd64.tar.gz -C releases/darwin-amd64 $(.APP_NAME)

	@echo "\033[32mMake release file finished.\033[0m\n"

release-darwin-arm64:
	@echo "\033[36mdarwin-arm64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf releases/darwin-arm64
	@mkdir -p releases/darwin-arm64

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=darwin GOARCH=arm64 go build -o releases/darwin-arm64/$(.APP_NAME) $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@tar -zcf releases/darwin-arm64/$(.APP_NAME)_$(.APP_VERSION)_darwin_arm64.tar.gz -C releases/darwin-arm64 $(.APP_NAME)

	@echo "\033[32mMake release file finished.\033[0m\n"

release-linux-amd64:
	@echo "\033[36mlinux-arm64\033[0m"

	@echo "\033[33mRemaking release dir...\033[0m"
	@rm -rf releases/linux-amd64
	@mkdir -p releases/linux-amd64

	@echo  "\033[33mBuilding binary file...\033[0m"
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o releases/linux-amd64/$(.APP_NAME) $(.BUILD_FLAGS)

	@echo "\033[33mPacking archive file...\033[0m"
	@tar -zcf releases/linux-amd64/$(.APP_NAME)_$(.APP_VERSION)_linux_amd64.tar.gz -C releases/linux-amd64 $(.APP_NAME)

	@echo "\033[32mMake release file finished.\033[0m\n"

release-all: release-darwin-amd64 release-darwin-arm64 release-linux-amd64