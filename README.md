# 2JAE22.github.io

# Ruby 환경 설정 및 Jekyll 실행 방법

1. Ruby 설치  
   Ruby가 시스템에 설치되어 있는지 확인하세요.

2. Ruby 및 Gem 버전 확인  
   ```
   ruby -v
   gem -v
   ```

3. Bundler 설치  
   ```
   gem install bundler
   ```

4. Bundler 버전 확인  
   ```
   bundler -v
   ```

5. 프로젝트 의존성 설치  
   (프로젝트 폴더에서 실행)
   ```
   bundle install
   ```

6. Jekyll 로컬 서버 실행  
   ```
   bundle exec jekyll serve
   ```


| 용어 | 역할/정의 | 언제 쓰나 | 비고 |
|---|---|---|---|
| Ruby | 프로그래밍 언어 | Jekyll, Rails 같은 Ruby 기반 툴/프레임워크 구동 | Windows에선 RubyInstaller로 설치 |
| gem | Ruby 패키지(라이브러리) 단위. RubyGems는 패키지 관리자 | `gem install <패키지>` 로 개별 설치 | npm의 패키지, pip의 패키지와 비슷 |
| Bundler (`bundle`) | 프로젝트 단위 의존성 관리 도구 | `bundle install`로 `Gemfile`에 적힌 gem 일괄 설치, `bundle exec <명령>`으로 해당 버전 사용 | npm/yarn, pipenv와 비슷한 역할 |
| Jekyll | Ruby로 만든 정적 사이트 생성기 | 블로그/문서 사이트를 마크다운으로 빌드할 때 | GitHub Pages 기본 엔진. 실행은 보통 `bundle exec jekyll serve` |

요약 흐름: Ruby 설치 → Bundler 설치(`gem install bundler`) → 프로젝트 폴더에서 `bundle install` → 로컬 실행 `bundle exec jekyll serve`.