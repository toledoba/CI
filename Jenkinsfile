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
      AR2TOOL      = 'v.1.0'

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
          //def files = findFiles(glob: '**/*.owl') echo "${files[0].name} ${files[0].path} ${files[0].directory} ${files[0].length} ${files[0].lastModified}"
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
            echo "Building Widoco version ${WIDOCO}"
          }
          //java -jar widoco-VERSION-jar-with-dependencies.jar [-ontFile file] or [-ontURI uri] [-outFolder folderName] [-confFile propertiesFile] or [-getOntologyMetadata] [-oops] [-rewriteAll] [-crossRef] [-saveConfig configOutFile] [-useCustomStyle] [-lang lang1-lang2] [-includeImportedOntologies] [-htaccess] [-webVowl] [-licensius] [-ignoreIndividuals] [-analytics analyticsCode] [-doNotDisplaySerializations][-displayDirectImportsOnly] [-rewriteBase rewriteBasePath] [-excludeIntroduction] [-uniteSections]
        }
        sh "java -jar widoco-${WIDOCO}-jar-with-dependencies.jar -ontFile Ontology/alo.owl -outFolder doc  -oops -rewriteAll -lang en-es"
        
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
        script{
          def exists = fileExists "ar2dtool-0.1.jar"
          if(!exists){
            sh "wget https://github.com/idafensp/ar2dtool/archive/${AR2TOOL}.tar.gz"
            sh "tar -xf ${AR2TOOL}.tar.gz"
            sh "rm ${AR2TOOL}.tar.gz"
            sh "mv ar2dtool-${AR2TOOL}/lib/ar2dtool-0.1.jar . "
            sh "rm -rf ar2dtool-${AR2TOOL}"
          }else{
             echo "Building AR2Tool version ${AR2TOOL}"
          }

        }
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


