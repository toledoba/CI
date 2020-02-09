/*******************************************************\
    Universidad Politecnica de Madrid, Spain
    Copyright 2020 Ontology Engineering Group
    @autor: 
\*******************************************************/

// -- Directory where the Project Files are located.  
def JOB_FILES_DIRECTORY
// -- Directory where the Platform Tools is located
def PLATFORM_TOOL_DIRECTORY
// -- Path of the Suite to execute
def SUITE_PATH


pipeline {

  agent {
      label '!windows'
  }
  // -- Display a timestamp on the log.
  options{timestamps()}
  // -- Evironment
  environment {
      //DISABLE_AUTH = 'true'
      //DB_ENGINE    = 'sqlite'
      VERSION      = 'undefined'
      WIDOCO       = '1.4.13'
      AR2TOOL      = 'ar2dtool-0.1'

  }

  stages {

    // Parameters needed: JOB_FILES_DIRECTORY, PLATFORM_TOOL_DIRECTORY, EMULATOR_DIRECTORY, SUITE_PATH
    // JOB_NAME, JOB_APPIUM_SUITE
    // ------------------------------------
    // -- STAGE: Initial Configuration
    // ------------------------------------
    stage("Initial Configuration") {
      steps {
        
        script {

          if (isUnix()) {
            //TODO
            //sh "'${mvnHome}/bin/mvn' -Dintegration-tests.skip=true -Dbuild.number=${targetVersion} clean package"
            echo "Unix"
            echo "${env.WORKSPACE}"
          } else {
            //TODO
            //bat(/"${mvnHome}\bin\mvn" -Dintegration-tests.skip=true clean package/)
            //print pom.version
            print "Windows"
            //sh('mkdir jhon')
            // -- Path Workspace
            echo "${env.WORKSPACE}"

          } 
            // -- Set the Directory of the files in the workspace
            JOB_FILES_DIRECTORY = "${env}"
            echo "directorio $JOB_FILES_DIRECTORY"
            // -- Set the suite name and route parameter
            //SUITE_PATH = "src/test/resources/suites/"+"${JOB_APPIUM_SUITE}"+".xml" 
        }
        // -- Clean Workspace
        echo "Clean Workspace"
        //cleanWs()
        
      }
    }
    // Parameters needed:
    // ------------------------------------
    // -- STAGE: Widoco
    // ------------------------------------
    stage('Widoco'){
      steps{
        script{
          def exists = fileExists "widoco-${WIDOCO}-jar-with-dependencies.jar"
          if (!exists) {
            sh "wget https://github.com/dgarijo/Widoco/releases/download/v${WIDOCO}/widoco-${WIDOCO}-jar-with-dependencies.jar"
          } else {
            echo "Building Widoco version ${VERSION}"
          }

        }
        
        //git url: 'https://github.com/dgarijo/Widoco'
        //sh('mvn install -DskipTests')
        //script{
        //  def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
        //  if (matcher) {
        //    VERSION = "${matcher[0][1]}"
        //    echo "Building Widoco version ${VERSION}"
        //  }
        //}
        //sh("mv jar/widoco-${VERSION}-jar-with-dependencies.jar .")
        //sh ("java -jar widoco-1.4.13-jar-with-dependencies.jar -ontFile alo.owl -outFolder doc -confFile ./config/ontosoft.properties -rewriteAll -lang en;es") 
        
      }
    }
    // Parameters needed:
    // ------------------------------------
    // -- STAGE: Oops!
    // ------------------------------------
    stage('Oops!') {
      steps {
        sh 'pwd'
//        echo "Database engine is ${DB_ENGINE}"
//        echo "DISABLE_AUTH is ${DISABLE_AUTH}"
//        sh 'printenv'
        //sh './widoco.sh'
      }
    }
    // Parameters needed:
    // ------------------------------------
    // -- STAGE: AR2Tool
    // ------------------------------------
    stage('AR2Tool') {
      steps {
        sh 'pwd'
        //sh 'wget https://github.com/idafensp/ar2dtool/archive/v.1.0.tar.gz'
        //sh 'tar -xf v.1.0.tar.gz'
        //sh 'mv ar2dtool-v.1.0/lib/ar2dtool-0.1.jar .'
        //git url: 'https://github.com/idafensp/AR2DTool/'
        //sh("mv lib/ar2dtool-0.1.jar .")
        //sh('java -jar ar2dtool.jar -i PathToInputRdfFile -o FileToOutputFile -t OutputFileType -c PathToConfFile -GENERATE_FLAGS [-d]')
        //sh('mvn install')

      }
    }
    // Parameters needed:
    // ------------------------------------
    // -- STAGE: VocabLite
    // ------------------------------------
    stage('VocabLite') {
      steps {
        sh 'pwd'
      }
    }
  }
}


