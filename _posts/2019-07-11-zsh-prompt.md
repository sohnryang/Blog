---
layout: post
title: Making My Own Zsh Prompt
tags: [zsh, programming, shell, cli]
---

[여러](https://github.com/sindresorhus/pure) [가지](https://github.com/marszall87/lambda-pure) [zsh](https://github.com/romkatv/powerlevel10k) [prompt](https://github.com/agnoster/agnoster-zsh-theme)를 사용한 뒤, 내가 직접 하나 만들어 봐야겠다는 생각이 들었다.

사실 이번이 처음은 아니다. [예전에 한 번 만들었다 버린 prompt](https://github.com/sohnryang/fattyarrow)도 있고, 내 programming bucketlist에 오랫동안 있기도 했다. 이번에는 어떻게 zsh prompt를 만드는지, 나는 어떻게 만들었는지를 정리해 보았다.

## Design
zsh prompt는 사실 그렇게 복잡하지는 않다. `PROMPT` 변수에 어떤 prompt를 보여줄지만 정해서 넣어주면 끝난다. 예를 들어, 다음과 같은 초간단 prompt를 만드는 것도 가능하다.

```shell
PROMPT='=> '
```

한줄이면 끝이다. 물론 이 prompt는 git branch는 고사하고, 내가 어떤 directory에 있는지도 보여주지 않으므로, 거의 쓸모가 없다. 이건 취향의 문제이지만, 어쨌든 내가 만든 prompt는 내가 사용할 예정이었으므로 다음과 같은 정보는 표시할 수 있어야 했다.

- 저번 명령이 실패했는지/아닌지
- git branch
- virtualenv name
- current directory

물론, 나중에는 더 추가할 수도 있을 것이다. 일단 이렇게 한번 만들어 보자.

우선 prompt symbol은 람다로 하기로 했다. 람다가 좋아서이기 때문이다.

그리고, 명령어를 치는 곳 윗줄에는 현재 디렉토리, git branch, virtualenv 등의 정보를 보여주는 것으로 디자인을 했다.

## Implementation

### Last Command Success/Fail
이 부분은 꽤 간단했다. 다음과 같은 코드를 사용하면 된다. ~~[다른 prompt](https://github.com/robbyrussell/oh-my-zsh/blob/master/themes/robbyrussell.zsh-theme) 코드 배꼈다는게 함정~~

```shell
local lambda_color="%(?:%{$fg[yellow]%}:%{$fg[red]%})"
```

마지막 command의 return code를 확인하여, 0이 아니면 람다가 빨갛게 보인다. 0인 경우에는 노랗게 보인다.

### Git Branch
git branch를 가져오는 방법은 많은데, 가장 좋은 것은 oh-my-zsh의 `git_prompt_info`를 사용하는 방법이다. 애초에 prompt에 사용할 목적으로 만들어진 유틸리티이다. 다음과 같이 환경 변수를 세팅하면 내가 굳이 formatting을 안해도 된다.

```shell
ZSH_THEME_GIT_PROMPT_PREFIX=" %{$fg[cyan]%}"
ZSH_THEME_GIT_PROMPT_SUFFIX="%{$reset_color%}"
ZSH_THEME_GIT_PROMPT_DIRTY="*"
ZSH_THEME_GIT_PROMPT_CLEAN=""
```

### Virtualenv
oh-my-zsh의 virtualenv plugin을 사용하면 `virtualenv_prompt_info`라는 것을 사용할 수 있고, `git_prompt_info`와 비슷하게 사용할 수 있다.

```shell
ZSH_THEME_VIRTUALENV_PREFIX=" %{$fg[green]%}"
ZSH_THEME_VIRTUALENV_SUFFIX="%{$reset_color%}"
```

## Finish & Release
이렇게 다 끝내고 나서, 이렇게 보인다.

![screenshot](https://rawcdn.githack.com/sohnryang/lambda-minimal-theme/ec441881d3c355c4d377edd4a08e59cf89924221/screenshot.png)

[여기](https://github.com/sohnryang/lambda-minimal-theme)에서 한 번씩 써 보고, 피드백을 주었으면 좋겠다. ~~스타도 주면 좋겠다.~~
