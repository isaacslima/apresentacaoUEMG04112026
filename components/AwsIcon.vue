<script setup lang="ts">
// Ícones oficiais dos serviços AWS (pacote @iconify-json/logos)
import Aws from '~icons/logos/aws'
import ApiGateway from '~icons/logos/aws-api-gateway'
import CloudFront from '~icons/logos/aws-cloudfront'
import CloudWatch from '~icons/logos/aws-cloudwatch'
import Ec2 from '~icons/logos/aws-ec2'
import Ecs from '~icons/logos/aws-ecs'
import Elb from '~icons/logos/aws-elb'
import Fargate from '~icons/logos/aws-fargate'
import Lambda from '~icons/logos/aws-lambda'
import S3 from '~icons/logos/aws-s3'

defineProps<{ name: string }>()

const icons: Record<string, any> = {
  'aws': Aws,
  'api-gateway': ApiGateway,
  'cloudfront': CloudFront,
  'cloudwatch': CloudWatch,
  'ec2': Ec2,
  'ecs': Ecs,
  'elb': Elb,
  'fargate': Fargate,
  'lambda': Lambda,
  's3': S3,
}
</script>

<template>
  <component :is="icons[name]" class="inline-block" />
</template>
