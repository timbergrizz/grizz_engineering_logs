- Nest는 미들웨어가 아닌 모듈이 중심이 된다.
	- 앞으로 모듈을 많이 만들게 될 것.
- express 강의에서 사용했던 라우터들을 그대로 옮겨보자.
	- TypeORM도 알아야 세부적으로 사용할 수 있기 때문에 모두 옮기지는 않겠지만, 일단은 해보자.
- Swagger 자동 생성 / decorator 쓰는거 중심으로 한번 알아보자.
- Nest에서는 다음과 같이 ```nest generate``` 명령어를 통해 자동으로 파일을 생성하고 import할 수 있다.![[Screenshot 2022-10-07 at 16.19.40.png]]
	- app.module.ts에 자동으로 연결된 것을 확인할 수 있다.![[Screenshot 2022-10-07 at 16.20.10.png]]
- 다음과 같이 controller 클래스를 만들 수 있다.
	```ts
	import { Controller, Get, Post } from '@nestjs/common';

	@Controller('users')
	export class UsersController {
	    @Get()
	    getUsers() {}
	
	    @Post()
	    postUsers() {}
	
	    @Post(`login`)
	    login() {}
	
	    @Post('logout')
	    logout() {}
	}
	```
	- 프론트에서 주소에 데이터 / 쿼리 / 파일 등을 같이 보낼 수 있다.
	- 어떨 것을 받을지 생각해볼 필요가 있다.
- getUsers에서는 지금 로그인한 사용자 정보를 가져오는 api이다.
- Nest에서는 어떤 프레임워크를 쓰는지 중요하지 않도록 설계해야 한다.
	- 최대한 다른 프레임워크에 의존성을 가지지 않도록 설계하는 것이 좋다.
- Nest에서 기반 프레임워크는 중요하지 않다.
	- 나중에 다른 프레임워크가 붙어도 작동에 지장이 없도록 최대한 설계해야 한다.
	- 컨트롤러에는 최대한 request 안쓰는게 좋다는 뜻이다.;
- 내부적으로 이루어지는 프로세스에 대해 의문을 가지지 않아도 된다.
	- 원리는 알아야 하는데 구체적인 구현을 알 필요는 없다.
- Nest에서는 export default가 아닌 export를 사용하고, interface가 아닌 class를 사용하여 export한다.
	- interface는 typescript에만 존재하고, 컴파일 이후 사라진다.
	- 클래스는 js로 바뀐 후에 런타임에도 남아있기 때문에 이렇게 작동하는 것이 적절할 수 있다.
- DTO를 만들때의 장점이 많다.
	- 