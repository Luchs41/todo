<template>
	<nav class="navbar navbar-light" style="background-color:gray">
		<div class="container-fluid">
			<span class="navbar-brand mb-0 h1 text-light">To Do List</span>
		</div>
	</nav>
	<div class="card my-4" style="width: 80%; left: 10%">
		<div class="card-header" style="background-color:#FFEB46; ">
			할 일은 제 때 하자에요
		</div>
		<div class="card-body row">
			<div class="col-3">
				<img class="img-fluid rounded" src="http://file3.instiz.net/data/cached_img/upload/2020/06/04/13/09f38567eef334085dc93741325cc3c9.jpg">
			</div>
			<div class="col">
				<p>
					이건영의 Todo List 입니다. 
				</p>
				<div>오늘은 {{ today.year }}년 {{ today.month }}월 {{ today.date }}일 입니다. </div>
				<div>할 일은 제 때 끝내는 어른이 되어요. </div>
			</div>
		</div>
	</div>

	<div style="margin-bottom:100px">
		<div class="card" style="width: 90%; left: 5%">
			<ul class="list-group list-group-flush">
				<li class="list-group-item listhead">
					<div class="row">
						<div class="col-2" style="text-align:center">
							Finished
						</div>
						<div class="col-7">
							Content
						</div>
						<div class="col-3">
							Due to
						</div>
					</div>
				</li>
				<li class="list-group-item" v-for="(a, i) in list" :key="i">
					<div class="row">
						<div class="col-2 checking">
							<input type="checkbox" style="width : 25px; height : 25px;" v-model="list[i].isFinished">
						</div>
						<div class="col-7" :class="{finished : list[i].isFinished}">
							{{ list[i].content }}
						</div>
						<div class="col-3">
							{{ list[i].due.year }} / {{ list[i].due.month }} / {{ list[i].due.date }}
						</div>
					</div>
				</li>
			</ul>
		</div>
	</div>

	<button type="button" class="btn btn-lg newbutton" data-bs-toggle="modal" data-bs-target="#exampleModal">
		+ 할 일 추가
	</button>
	<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h5 class="modal-title" id="exampleModalLabel">
						할 일 추가하기
					</h5>
					<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
				</div>
				<div class="modal-body">
					<form>
						<div class="mb-3">
							<label for="message-text" class="col-form-label">내용</label>
							<textarea class="form-control" id="message-text" v-model="inputContent"></textarea>
						</div>
						<div class="mb-3">
							<label for="recipient-name" class="col-form-label">마감일</label>
							<input type="date" class="form-control" id="recipient-name" v-model="inputDateOrigin">
						</div>
					</form>
				</div>
				<div class="modal-footer">
					<button type="button" class="btn" data-bs-dismiss="modal" style="background-color : #dcdcdc">
						닫기
					</button>
					<button @click="addNewList" type="button" class="btn" data-bs-dismiss="modal" style="background-color : #FFEB46">
						추가하기
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import list from './assets/list.js'

export default {
  name: 'App',
	data(){
		return{
			list : list,
			today : {
				year : 0,
				month : 0,
				date : 0,
			},
			isModalOpen : true,
			inPutContent : '',
			inputDateOrigin : '',
		}
	},
  components: {
  },
	methods : {
		addNewList(){
			let newList = {
				isFinished : false,
				content : this.inputContent,
				due :{
					year : 0,
					month : 0,
					date : 0,
				}			
			};
			console.log(newList.content);
			console.log(this.inputDateOrigin);
			let inputDate = new Date(this.inputDateOrigin);
			console.log(inputDate);
			newList.due.year = inputDate.getFullYear();
			newList.due.month = inputDate.getMonth() + 1;
			newList.due.date = inputDate.getDate();
			this.list.push(newList);
			this.inputContent = '';
			this.inputDateOrigin = '';
		}
	},
	mounted(){
		let gettoday = new Date();
		this.today.year = gettoday.getFullYear();
		this.today.month = gettoday.getMonth();
		this.today.date = gettoday.getDate();
	}
}
</script>

<style>
.listhead{
font-size : 16pt;
color : white;
background-color: gray;
}
.checking{
text-align: center;
}
.finished{
text-decoration: line-through;
color: grey;
}
.newbutton{
display:scroll;
position: fixed;
bottom:30px;
right: 30px;
background-color: black;
color : whitesmoke;
}

</style>
