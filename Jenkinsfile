node {
  checkout scm

  stage 'Deploy application release'
  writeFile file: 'extras.json', text: "{'image_tag':'${IMAGE_TAG}','ecs_tasks':[${TASKS}]}"
  sh 'ansible --version'

  withEnv(["VAULT_PASSWORD=${VAULT_PASSWORD}"]) {
    sh 'python vault.py'
    sh 'ansible-playbook site.yml --vault-password-file vault.py -e "@extras.json"'
  }
}