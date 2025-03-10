pipeline {
    agent any
    tools {
        maven 'M3_8_6'
    }
    stages {
        
        stage('Zuul') {
            steps {
                dir("ZuulBase/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t tonabarrera/zuul:latest ."
                        sh 'docker stop zuul || true'
                        sh 'docker run -d --rm --name zuul -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.100.5 -p 8000:8080 tonabarrera/zuul:latest'
                        //sh 'docker push tonabarrera/zuul:latest'
                    }
                }
            }
        }

        stage('Eureka') {
            steps {
                dir("EurekaBase/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t tonabarrera/eureka:latest ."
                        sh 'docker stop eureka || true'
                        sh 'docker run -d --rm --name eureka -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.100.5 -p 8761:8761 tonabarrera/eureka:latest'
                        //sh 'docker push tonabarrera/eureka:latest'
                    }
                }
            }
        }
        
        stage('Ordenes') {
            steps {
                dir("ordenes-service/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t tonabarrera/ordenes-service:latest ."
                        sh 'docker stop ordenes-service || true'
                        sh 'docker run -d --rm --name ordenes-service -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.100.5 -p 8020:8020 tonabarrera/ordenes-service:latest'
                        //sh 'docker push tonabarrera/ordenes-service:latest'
                    }
                }
            }
        }

        stage('Productos') {
            steps {
                dir("productos-service/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t tonabarrera/productos-service:latest ."
                        sh 'docker stop productos-service || true'
                        sh 'docker run -d --rm --name productos-service -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.100.5 -p 8030:8030 tonabarrera/productos-service:latest'
                        //sh 'docker push tonabarrera/productos-service:latest'
                    }
                }
            }
        }

        stage('Usuarios') {
            steps {
                dir("usuarios-service/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t tonabarrera/usuarios-service:latest ."
                        sh 'docker stop usuarios-service || true'
                        sh 'docker run -d --rm --name usuarios-service -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.100.5 -p 8010:8010 tonabarrera/usuarios-service:latest'
                        //sh 'docker push tonabarrera/usuarios-service:latest'
                    }
                }
            }
        }
    }
}