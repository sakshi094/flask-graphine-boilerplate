# flask-graphine-boilerplate
Use of graphQL with Flask
cd flask-graphine-boilerplate

# Create a virtualenv to isolate our package dependencies locally
virtualenv env
source env/bin/activate  # On Windows use `env\Scripts\activate`

# SQLAlchemy and Graphene with SQLAlchemy support
pip install SQLAlchemy
pip install graphene_sqlalchemy

# Install Flask and GraphQL Flask for exposing the schema through HTTP
pip install Flask
pip install Flask-GraphQL

*Create Some data*
$ python

>>> from .models import engine, db_session, Base, Department, Employee
>>> Base.metadata.create_all(bind=engine)

>>> # Fill the tables with some data
>>> engineering = Department(name='Engineering')
>>> db_session.add(engineering)
>>> hr = Department(name='Human Resources')
>>> db_session.add(hr)

>>> peter = Employee(name='Peter', department=engineering)
>>> db_session.add(peter)
>>> roy = Employee(name='Roy', department=engineering)
>>> db_session.add(roy)
>>> tracy = Employee(name='Tracy', department=hr)
>>> db_session.add(tracy)
>>> db_session.commit()

*Testing our GraphQL schema*
$ python ./app.py

 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 
 Go to localhost:5000/graphql and type your first query!
 type below in left side of browswer and run it
 {
  allEmployees {
    edges {
      node {
        id
        name
        department {
          name
        }
      }
    }
  }
}
