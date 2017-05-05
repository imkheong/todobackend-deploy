node {
  checkout scm

  stage 'Deploy application release'
  writeFile file: 'extras.json', text: "{'image_tag':'${IMAGE_TAG}','ecs_tasks':[${TASKS}]}"
  sh 'cat extras.json'
  sh 'ansible --version'

  withEnv(["VAULT_PASSWORD=${VAULT_PASSWORD}"]) {    
    sh 'ansible-playbook site.yml --vault-password-file vault.py -e "@extras.json"'
  }
}