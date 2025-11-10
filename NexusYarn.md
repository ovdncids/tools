# Nexus (3.86.0-08)
* https://help.sonatype.com/en/install-nexus-repository-with-postgresql.html
* nexus-3.86.0-08\etc\nexus-default.properties > host와 port 설정

## Proxy
* 그대로 토스 하는 역할을 한다. `https://registry.yarnpkg.com`은 `https://registry.npmjs.org`의 `Proxy`이다.
```sh
Nexus > Settings > Repositories> Create Repository > npm (poxy)
Name: npm-proxy
Remote storage: https://registry.npmjs.org/
```
* http://localhost:8081/repository/npm-proxy/react

.yarnrc
```yarnrc
registry "http://localhost:8081/repository/npm-proxy/"
```
```sh
# yarn add 상세 정보 보기
yarn add react --verbose > yarn-log.txt
```

## Hosted
* 내부 라이브러리를 등록 한다.
```sh
해당 프로젝트 > yarn pack > 프로젝트-버전.tgz 생성

Nexus > Settings > Repositories> Create Repository > npm (hosted)
Name: npm-hosted
```
* `프로젝트-버전.tgz 파일` 등록

.yarnrc
```yarnrc
registry "http://localhost:8081/repository/npm-hosted/"
```
```sh
yarn add 프로젝트
```

## Group
* Proxy와 Hosted를 혼합한다.
```sh
Nexus > Settings > Repositories> Create Repository > npm (group)
Name: npm-group
Group Member repositories: npm-proxy + npm-hosted
```
.yarnrc
```yarnrc
registry "http://localhost:8081/repository/npm-group/"
```

* 이제 Proxy와 Hosted 둘다 사용가능하다.

# YARN
## 해당 라이브러리 버전으로 lock 해서 yarn install 하기
package.json
```json
{
  "resolutions": {
    "minimatch": "3.0.4"
  }
}
```

## yarn.lock 파일을 lock 해서 yarn install 하기
```sh
yarn install --frozen-lock
```

## `yanr install` Request failed "401 Unauthorized"
* https://github.com/yarnpkg/yarn/issues/3093
* C:\Users\[사용자]\.npmrc (파일 첫 줄에 추가)
```npmrc
always-auth=true
```
