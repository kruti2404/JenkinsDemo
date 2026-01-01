pipeline {
	agent any 

	environment {
		DOTNET_CLI_HOME= "C:\\Program Files\\dotnet"
	}

	stages{
		stage('Checkout'){
			steps{
				checkout scm
			}
		}
		stage('Restore'){
			steps{
				script{
					bat "dotnet restore"
				}
			}
		}

		stage('Build'){
			steps{
				script{
					bat "dotnet build --no-restore --configuration Release"
				}
			}
		}

		stage('Test'){
			steps{
				script{
					bat "dotnet test --no-build --configuration Release"
				}
			}
		}

		stage('Publish'){
			steps{
				script{
					bat "dotnet test --no-test --configuration Release --output .//publish"
				}
			}
		}

		stage('Run'){
			steps{
				 bat """
                cd publish
                dotnet WebApp.dll
                """
			}
		}
	}

	post {
		success{
			echo "Build, Test, Publish and Run Successfull"
		}
	}
}