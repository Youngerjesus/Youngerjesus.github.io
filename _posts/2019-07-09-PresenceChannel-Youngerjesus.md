---
layout: post
title:  "Presence Channel"
date:   2019-07-09 12:36:36 +0530
---
Presence Channel 만드는 과정 
1. Database -> migration 작업( 아마 테이블만드는 작업인거같다)
	팀 단위로 데이터베이스 수정을 할 수 있도록 해주는것 그리고 데이터베이스 스키마를 공유할 수 있도	록 해주는것, 스키마를 만들 수 있도록해주는것 

	up() 메소드 
		데이터베이스에 테이블 칼럼 인덱스를 추가하는데 사용되고 
	down() 메소드 
		단순히 up 메소드의 동작을 취소한다. 
		(왜 다운이 있는거지? 그냥 up지우면되지않나)

2. User와 Message를 연결시키는 작업(Eloquent Relationship 만들기) 
	app -> User.php
		public function message() {
			return $this->hasMany(Message:class); // 데이터베이스 테이블 연결시키는관계만들기
		}
		
	일대일 relataionship 만들기 하나의 User 모델이 하나의 Phone과 관계되어 있을 수 있으니
	User모델에 phone 메소드를 구성한거 관계가 정의되면 해당 모델에 접근할 수있다. 
	$phone =. User::find(1) -> phone 이렇게 찾을 수 있다. 
		larval -> 와 ::의 차이는 뭔데 

	app -> Message.php
		protected $fillable = [‘messages’]
		public function user(){
			return $this->belongsTo(User::class); 
		}
	
	hasOne vs hasMany 
		결국 일대일관계 일대다 관계 다대다 관계 이거에 따라서 나뉜다. 

	$fillable = []
	대량할당 
		웹 어플리케이션에서 주로 하는일은 데이터베이스에 저장하거나 데이터베이스에 있는 내용을
		화면에 보여주는 일이 많다. 이때 요청을 할 때 HTML 폼이나 AJAX 요청등을 통해 사용자의 입력값을
		서버로 전송하거나 보통 배열로 변환된다. 
		왜 배열로 바로 받지않고 변환시키냐면 검사하는거다 배열로 바로 받으면 검사를 안하는거지. 
		검사한다는게 사용자가 넣으면 안되는 값을 말한다. 이렇기 때문에 
		Eloquent는 모델에 배열을 직접 전달하고 데이터베이스를 변경할떄 개발자가 명시적으로 
		사용자가 입력이 가능한 칼럼을 지정해줘야한다. 

		변경이 허락되지 않은 칼럼들에 대해서 값을 대량 할당하는 경우 발생하는 예외가 발생		MassAssignmentExceptionfillable 
		칼럼들에 대해 대량할당이 가능하게 하는것이 두가지 방식 
		
		fillable - 화이트 리스트 방식 
		모델의 $fillable 배열에 입력이 가능한 칼럼을 명시적으로 지정하는 방식 
		class Task extends Model {
			protected $fillable = [‘name’,’project_id’]; 
		}
		
		guarded - 블랙리스트 방식 
		모델의 $guarded변수는 보호해야할 칼럼을 명시적으로 지정하는 방식으로 여기에 지정되지 않은 칼럼은
		모두 값 설정이 가능하다. 
		(하나의 모델에서 $fillable, $guarded 모두 사용불가 한가지만 사용가능) 
3. Routes/web.php
	해당 요청에 컨트롤러 등록 
	Route::get(‘/chats’, ‘ChatsController@index’); 
	
	ChatsController@index에서 @index는 뭔데  ChatsController의 index메소드에 위임하겠다 라는거
 	
	리소스 컨트롤러와 그냥 컨트롤러의 차이는 어떻게되는데
		사용법 차이는 그냥 컨트롤러는 메소드까지 입력해줘야하는거 같은대
		리소스 컨트롤러는 한번의 선언만으로 Restful한 액션에 대해서 다양한 라우트를 설정하는게 가능하다.
		일반 컨트롤러는 각각의 액션에대해서 라우트를 다르게 선언해줘야한다. 
		예를들면 리소스 컨트롤러에서 get방식으로 오면 index메소드에서 실행하고 
		post방식으로오면 store 메소드로 실행한다. 
		
	컨트롤러 
		애플리케이션의 요청에 대한 모든 처리 로직을 하나의 routes.php 파일에 정의하는 것보다 
		별도의 컨트롤러 클래스를 통해서 구성하는것 가능 컨트롤러는 클래스를 구성해서 HTTP 요청에대한 
		그룹을 지정한다. 
		
	Axios 
		REST API 방식을 따라서 
		HTTP 클라이언트 라이브러리로써 비동기 방식으로 HTTP 데이터 요청을 하는것 
		
	Axios 사용법 
		Successdd이면 .then함수로, failure일 경우 catch()함수로 이동 
		Axios를 통해 가져오는 결과값을 항상 response
		API구조를 알고 있다면 JSON 형식으로 불러오는 것 가능 
	
4. ChatsController.php 에서 미들웨어를 사용하기 위해서 _construct() 등록 
	public function _construct() {
		$this -> middleware(‘auth’); 
	}

5. ChatsController.php 에서 index() 메소드 등록 
	public function index() {
		return view(‘chats’); 
	}

    view란 
        애플리케이션에서 제공하는 HTML로 구성되고 컨트롤러/애플리케이션 로직을 분리하기 위해서 사용한다 뷰파일은 resources/views 디렉토리에 위치한다. 

        예제 
        Route::get('/', function ()    {
            return view('greeting', ['name' => 'James']);
        }); 
        view의 첫번쨰 인자 greeting은 resources/view 디렉토리에 위치하는 파일의 이름이된다. 두번째인자는 뷰에서 사용하기위한 데이터들의 배열이다. 
        이러한 방식으로 데이터를 전달할 떄 항상 Key-Value로 구성된 배열이여야만 한다. 
    
    view가 blade file을 가리킨다 => blade 파일 양식은 커스터마이징 
    
6. 라우터에 message가 들어왔을때 chat컨트롤러의 가져오는, 보내는 메소드 정의  
    routes/web.php 
        Route::get('/messages','ChatsController@fetchMessage);
        Route::post('/messages', 'ChatsController@sendMessage); 

    controllers/Auth/ChatsController 
        + public function fetchMessage() { 
            return Message::with('user') -> get(); 
        } 

        +  public function sendMessage(Request $request) {
            auth()->user()->messages()->create({
                'message' => $request->message
            }); 

            return ['status' => 'success'];
        }

        fetchMessage()는 어떻게 동작하길래 메시지를 가져오는거지? 
            채팅방 로딩될떄 메시지 가져오는걸로 쓴다. 그래서 사용자와 연관시키는거고 


7. 6에서 만든 method vue 컴포넌트에서 쓰기 
    // script 
    export default {
        data() {
            return {
                messages: [],
                newMessage: ''
            }
        }, 

        created() {
            this.fetchMessage(); 
        }, 

        method() {
            fetchMessage() {
                axios.get('messages').then(response => {
                    this.messages = response.data; 
                })
            },

            sendMessage() {
                this.messages.push({
                    user: this.user 
                    message:this.messages
                }); 

                axios.post('messages', {message: this.newMessage});

                this.newMessage = ''; 
            }

        }
    }
    // html 
        v-for= "message in messages" 
            {{message.name}}
            {{message.message}}

8. message를 broadcast하기 
    event를 만들어야한다. => Events/MessageSent 만들기 
    
    MessagesSent implements ShouldBroadcast 

    public function broadcastOn(){ // Presence채널은 누가 있는지 알 수 있다. Private 채널과 비슷하지만 
        return new PresenceChannel('chat'); 
    }

    channel.php 
        // 만약 private 채널이라면 사용자가 이 채널에 입장여부가 확인되었었는지를 검증해야한다. PresenceChannel도 마찬가지 
        // 여기서는 true, false, 값 대신에 user가 있는지를 판단으로  
        Broadcast::channel('chat', function ($user) {
                return $user;
        });

9. controller에서 이벤트를 날리는게 아니라 broadcast 클래스를 만들어서 컨트롤러에서 이벤트를 날리네 
    ChatsController
        public function sendMessage(){
            + $message = auth() -> user() -> messages() -> create({
                'message' => $request-> message
            }); 

            +   broadcast(new MessageSent($message->load('user')) )->toOthers();  

        }
        load는 뭐지? 

    laravel PresenceChannel에 대해서 좀 더 알아야겟다. 
