node ('Slave') {
notifyStarted()
 stage ('Checkout')  {

     build job: 'CheckOut' 
 }
stage ('Build') {
     build job: 'Build' 
    }
stage ('Code Quality scan') {
      build job: 'Code_Quality' 
        }
        
stage('Archive Artifacts') {
build job: 'Archive_Artifacts'
}
 stage('Publish to Artifactory') {
build job: 'Publish_To_Artifactory'
}

stage ('Slack notification') {
     
build job: 'Slack_Notification'
    }
  
}
def notifyStarted() {
  def mailRecipients = "dtrailblazers21@gmail.com"
  // send to email
  
    def jobName = currentBuild.fullDisplayName

    emailext body: '''${SCRIPT, template="groovy-html.template"}''',
        mimeType: 'text/html',
        subject: "[Jenkins] ${jobName}",
        to: "${mailRecipients}",
        replyTo: "${mailRecipients}",
        recipientProviders: [[$class: 'CulpritsRecipientProvider']]
}
  def notifySuccessful() {
  def mailRecipients = "dtrailblazers21@gmail.com"


  emailext (
      subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]’",
      to: "${mailRecipients}",
      body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
      recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )
}