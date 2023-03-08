---
title: AWS 및 Azure에서 지속적 통합 및 지속적 배포
description: 
published: true
date: 2023-02-04T16:55:55.241Z
tags: 
editor: markdown
dateCreated: 2023-02-04T16:55:49.804Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Continuous Integration and Continuous Deployment on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/continuous-integration-and-continuous-deployment-on-aws-and-azure)
{.links-list}


# AWS 및 Azure에서 지속적 통합 및 지속적 배포

AWS 및 Azure와 같은 클라우드 플랫폼은 리소스를 빠르게 확장할 수 있는 기능과 다양한 프로그래밍 언어 및 도구를 사용할 수 있는 유연성을 포함하여 개발자에게 많은 이점을 제공합니다. 또한 이러한 플랫폼을 사용하면 CI(지속적인 통합) 및 CD(지속적인 배포) 파이프라인을 쉽게 설정할 수 있습니다.

이 기사에서는 AWS 및 Azure에서 CI/CD 파이프라인을 설정하는 방법을 살펴보겠습니다. 또한 CI/CD에 이러한 플랫폼을 사용할 때의 몇 가지 이점과 문제점에 대해서도 논의할 것입니다.

## 지속적인 통합이란 무엇입니까?

지속적 통합(CI)은 코드 변경이 있을 때 자동으로 빌드하고 테스트하는 방법입니다. 이를 통해 개발자는 오류를 신속하게 감지하고 수정할 수 있으며 코드 기반이 항상 배포 가능한 상태인지 확인하는 데 도움이 됩니다.

 CI 파이프라인은 일반적으로 코드 커밋에 의해 트리거되며 일반적으로 다음 단계를 포함합니다.

- 코드가 자동으로 빌드되고 테스트됩니다.
- 자동 테스트를 실행하여 오류를 확인합니다.
- 테스트를 통과하면 코드가 스테이징 환경에 배포됩니다.
- 테스트가 실패하면 코드가 배포되지 않고 개발자에게 알립니다.

## 지속적 배포란 무엇입니까?

연속 배포(CD)는 프로덕션 환경에 코드 변경 사항을 자동으로 배포하는 방법입니다. 이를 통해 개발자는 가능한 한 빨리 사용자에게 새로운 기능과 수정 사항을 제공할 수 있습니다.

CD 파이프라인에는 일반적으로 다음 단계가 포함됩니다.

- 코드가 자동으로 빌드되고 테스트됩니다.
- 테스트를 통과하면 코드가 프로덕션 환경에 배포됩니다.
- 테스트가 실패하면 코드가 배포되지 않고 개발자에게 알립니다.

## AWS에서 CI/CD 파이프라인 설정

AWS는 CI/CD 파이프라인을 설정하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 AWS CodePipeline 및 AWS CodeBuild를 사용하여 간단한 CI/CD 파이프라인을 설정하는 방법을 살펴보겠습니다.

### 전제 조건

시작하기 전에 다음이 필요합니다.

- AWS 계정
- GitHub 계정
- GitHub의 코드 저장소

### AWS CodePipeline 설정

AWS CodePipeline은 코드 변경 사항을 빌드, 테스트 및 배포하는 프로세스를 자동화하는 데 사용할 수 있는 서비스입니다.

CodePipeline을 사용하여 CI 파이프라인을 설정하려면 새 CodePipeline 파이프라인을 생성해야 합니다. 이렇게 하려면 AWS 콘솔에 로그인하고 CodePipeline 서비스로 이동합니다.

시작하려면 "파이프라인 생성" 버튼을 클릭하십시오.

"파이프라인 설정 선택" 페이지에서 파이프라인 이름을 지정하고 리전을 선택합니다. 그런 다음 "다음" 버튼을 클릭합니다.

"소스 추가" 페이지에서 "GitHub"를 소스 공급자로 선택합니다. 그런 다음 파이프라인에 사용할 리포지토리와 분기를 선택합니다. 마지막으로 "다음" 버튼을 클릭합니다.

"빌드 단계 추가" 페이지에서 "AWS CodeBuild"를 빌드 공급자로 선택합니다. 그런 다음 빌드 단계의 이름을 선택하고 "다음" 버튼을 클릭합니다.

"빌드 단계 구성" 페이지에서 "Linux, Ubuntu" 운영 체제 및 "표준" 런타임을 선택합니다. 그런 다음 "aws/codebuild/standard:4.0" 이미지를 선택합니다.

"EnvironmentVariables" 섹션에서 다음 환경 변수를 추가합니다.

- "이름": "REPOSITORY_NAME"
- "값": "GitHub 리포지토리 이름"

"BuildSpec" 섹션에서 다음 빌드 명령을 입력합니다.

- "버전: 0.2"
- "단계:"
- "pre_build:"
- "명령:"
- "echo GitHub에 로그인하는 중..."
- "${{git-credential}} 채우기"
- "짓다:"
- "명령:"
- "`날짜`에 시작된 에코 빌드"
- "에코 건설 현장..."
- "휴고"
- "post_build:"
- "명령:"
- "`날짜`에 에코 빌드 완료"

빌드 프로젝트를 저장하려면 "빌드 프로젝트 저장" 버튼을 클릭하십시오.

"배포 단계 추가" 페이지에서 "AWS CodeDeploy"를 배포 공급자로 선택합니다. 그런 다음 배포 단계의 이름을 선택하고 "다음" 버튼을 클릭합니다.

"배포 단계 구성" 페이지에서 "EC2/온프레미스" 인스턴스 유형과 "기본" 배포 유형을 선택합니다. 그런 다음 다음 배포 구성을 입력합니다.

- "애플리케이션 이름": "GitHub 리포지토리 이름"
- "배포 그룹 이름": "GitHub 리포지토리 이름-deploy"
- "서비스 역할 ARN": "arn:aws:iam::aws:policy/service-role/AWSCodeDeployRole"

"배포 그룹 저장" 버튼을 클릭하여 배포 그룹을 저장합니다.

"검토" 페이지에서 파이프라인 설정을 검토한 다음 "파이프라인 생성" 버튼을 클릭합니다.

이제 CI 파이프라인을 사용할 준비가 되었습니다. 코드 변경 사항을 GitHub 리포지토리에 커밋할 때마다 CodePipeline이 자동으로 코드를 빌드하고 배포합니다.

## Azure에서 CI/CD 파이프라인 설정

Azure는 CI/CD 파이프라인을 설정하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 Azure DevOps 및 Azure Pipelines를 사용하여 간단한 CI/CD 파이프라인을 설정하는 방법을 살펴보겠습니다.

### 전제 조건

시작하기 전에 다음이 필요합니다.

- Azure 계정
- GitHub 계정
- GitHub의 코드 저장소

### Azure DevOps 설정

Azure DevOps는 코드 변경 사항을 빌드, 테스트 및 배포하는 프로세스를 자동화하는 데 사용할 수 있는 서비스입니다.

Azure DevOps를 사용하여 CI 파이프라인을 설정하려면 새 Azure DevOps 프로젝트를 만들어야 합니다. 이렇게 하려면 Azure Portal에 로그인하고 Azure DevOps 서비스로 이동합니다.

시작하려면 "새 프로젝트" 버튼을 클릭하십시오.

프로젝트 이름을 지정한 다음 "만들기" 버튼을 클릭합니다.

이제 Azure DevOps 프로젝트를 사용할 준비가 되었습니다.

### Azure 파이프라인 설정

Azure Pipelines는 코드 변경 사항을 빌드, 테스트 및 배포하는 프로세스를 자동화하는 데 사용할 수 있는 서비스입니다.

Azure Pipelines를 사용하여 CI 파이프라인을 설정하려면 새 Azure Pipeline을 만들어야 합니다. 이렇게 하려면 Azure Portal에 로그인하고 Azure Pipelines 서비스로 이동합니다.

시작하려면 "새 파이프라인" 버튼을 클릭하십시오.

"소스 선택" 페이지에서 "GitHub"를 소스 공급자로 선택합니다. 그런 다음 파이프라인에 사용할 리포지토리와 분기를 선택합니다. 마지막으로 "계속" 버튼을 클릭합니다.

"템플릿 선택" 페이지에서 "스타터 파이프라인" 템플릿을 선택하고 "계속" 버튼을 클릭합니다.

"파이프라인 구성" 페이지에서 다음 YAML 코드를 입력합니다.

- 방아쇠:
- 가지:
- 포함하다:
- 주인
- 길: /
- readme.md
- 단계:
- - 단계: 빌드
- 작업:
- - 작업: 빌드
- 단계:
- - 체크아웃: 셀프
- - 작업: UseDotNet@2
- 입력:
- 패키지 유형: sdk
- 버전: 3.1.100
- - 작업: DotNetCoreCLI@2
- 입력:
- 명령: 빌드
- 인수: --configuration 릴리스
- - 단계: 테스트
- 작업:
- - 작업: 테스트
- 단계:
- - 체크아웃: 셀프
- - 작업: DotNetCoreCLI@2
- 입력:
- 명령: 테스트
- 인수: --no-build --configuration 릴리스
- - 단계: 배포
- 작업:
- - 작업: 배포
- 단계:
- - 체크아웃: 셀프
- - 작업: CopyFiles@2
- 입력:
- SourceFolder: '$(Pipeline.Workspace)'
- 내용물: '**/*'
- TargetFolder: '$(Build.ArtifactStagingDirectory)'
- - 작업: PublishBuildArtifacts@1
- 입력:
- 게시할 경로: '$(Build.ArtifactStagingDirectory)'
- ArtifactName: '드롭'
- publishLocation: '컨테이너'

"저장 및 실행" 버튼을 클릭하여 파이프라인을 저장하고 실행합니다.

이제 CI 파이프라인을 사용할 준비가 되었습니다. 코드 변경 사항을 GitHub 리포지토리에 커밋할 때마다 Azure Pipelines는 자동으로 코드를 빌드하고 배포합니다.

## 결론

이 기사에서는 AWS 및 Azure에서 CI/CD 파이프라인을 설정하는 방법을 살펴보았습니다. 또한 CI/CD에 이러한 플랫폼을 사용할 때의 몇 가지 이점과 문제점에 대해서도 논의했습니다.