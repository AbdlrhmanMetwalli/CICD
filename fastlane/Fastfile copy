# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

default_platform(:ios)



platform :ios do
  desc "run unit tests"
  lane :tests do |options|
    if options[:clone_source_packages]
      packages_path = "#{File.expand_path("..", Dir.pwd)}/cache/packages_cache"
      derived_data_path = "#{File.expand_path("..", Dir.pwd)}/cache/derived_data"

      scan(
          cloned_source_packages_path: packages_path,
          disable_package_automatic_updates: options[:disable_package_automatic_updates],
          skip_package_dependencies_resolution: options[:skip_package_dependencies_resolution],
	  derived_data_path: derived_data_path,
	  skip_build: options[:skip_build],
	  skip_testing: ["CICDTestUITests"],
       )
    else
      scan(
          disable_package_automatic_updates: options[:disable_package_automatic_updates],
          skip_package_dependencies_resolution: options[:skip_package_dependencies_resolution],
	  skip_testing: ["CICDTestUITests"],
       )
    end
  end

  desc "Run swiftlint"
  lane :lint do |options|
    swiftlint(
      mode: :lint,
      output_file: "swiftlint.result.json",
      raise_if_swiftlint_error: true,
      ignore_exit_status: false
    )
  end

end
