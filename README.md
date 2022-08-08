# https-c5.patreon.com-.circleci-config.yml-

version: 2.1
orbs:
  aws-cli: circleci/aws-cli@0.1.20

jobs:
  deploy_to_production:
    working_directory: ~/patreon_static
    parallelism: 1
    executor: aws-cli/default
    steps:
      - aws-cli/setup
      - checkout
      - run:
          name: Run deploy
          command: |
            ./deploy.sh

workflows:
  version: 2
  primary_workflow:
    jobs:
      - deploy_to_production:
          context: patreon_static
          filters:
            branches:
              only: master
