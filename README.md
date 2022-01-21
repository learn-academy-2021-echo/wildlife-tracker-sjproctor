# Rails API

- Just the M&C
- NO views! Just data

Project Instructions
- $ rails new wildlife-tracker -d postgresql -T
- $ cd wildlife-tracker
- $ git remote add origin https://github.com/learn-academy-2021-echo/wildlife-tracker-sjproctor.git
- $ git checkout -b main
- $ git add .
- $ git commit -m 'initial commit'
- $ git push origin main
- $ bundle add rspec-rails
- $ rails generate rspec:install


Only need the model and controller
- Student - name, cohort
- $ rails g resource Student name:string cohort:string

Resource creates:
- model
- controller
- spec files
- all restful routes

Postman
- Using Postman to visualize data output
- Headers tab - key: content-type, value: application/json
- Go back to params tab
- If you get HTML as a response, check the visualize tab


INDEX
- controller
```
def index
  student = Student.all
  render json: student
end
```

SHOW
- controller
```
def show
  student = Student.find(params[:id])
  render json: student
end
```

CREATE
- controller
- add to ApplicationController: `skip_before_action :verify_authenticity_token`
```
def create
  student = Student.create(student_params)
  if student.valid?
    render json: student
  else
    render json: student.errors
  end
end

private
def student_params
  params.require(:student).permit(:name, :cohort)
end
```

UPDATE
- controller
```
def update
  student = Student.find(params[:id])
  student.update(student_params)
  if student.valid?
    render json: student
  else
    render json: student.errors
  end
end
```

DESTROY
- controller
```
def destroy
  student = Student.find(params[:id])
  if student.destroy
    render json: student
  else
    render json: student.errors
  end
end
```
