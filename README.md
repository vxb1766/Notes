Refer: https://reacttraining.com/react-router/web/guides/philosophy
Structure of the project:
```
Blogs - this contains nothing but the navbar and routing setup which renders Posts Component on '/' {Posts}
  | - So when u land on '/', Routing renders Posts component (histor/location is available here). This Posts component is a collection of Post.
  | - withRouter is required because the history location is available at Posts, but not Post.
  v
Posts 
  |
  |
  v
Post




# Notes For React Router
Code : Udemy React course 

import React, {Component} from 'react';
import {BrowserRouter} from 'react-router-dom'; //This needs to be present in app.js/index.js  not here.
import {withRouter} from 'react-router-dom';
import {Route,Link,NavLink} from 'react-router-dom'; //NavLink is same as Link

import Posts from './Posts/Posts';
import NewPost from './NewPost/NewPost';


class Blog extends Component {
    render() {
        return (
            <div className="Blog">
                <header>
                    <nav>
                        <ul>
                            /*Link: this is similar to <a href>*/
                            <li><Link to="/">Home</Link></li>
                            <li><NavLink to={{
                                activeClassName="my-active" // The advantage of using NavLink is=> 1) it adds class to the Nav element and then using activeClassName, u can style the nav item. 
                                activeClassName={{ //This is for inline styling
                                    color: '#ddd',
                                    textDecoration: 'underline'
                                }}
                                pathname: '/new-post',
                                hash: '#submit',
                                search: '?quick-submit=true'
                            }}>New Post</NavLink></li>

                            

                        </ul>
                    </nav>
                </header>
                <div>
                  <Post {...this.props} /> -------(a)
                </div>
                <Switch>  //Using switch will ensure only one route is rendered. if u donot use switch, since we donot use exacts, 2 or more routes url will match. Hence 2 components will be rendered on the same page.
                    <Route path="/" exact component={Posts}/>
                    <Route path="/new-post" component={NewPost}/>
                    <Route path="/:id" exact component={FullPost}/>
                </Switch>
            </div>
        );
    }
}

export default Blog;
//exports default withRouter(Posts) 
/*
withRouter is Required when routing props such as history/location etc needs to be passed to child. These are not passed by default
within the props property. One workaround is ------(a) i.e {...this.props}. this will Passdown all the propertis the component receives to child
*/


Note: Programatically <Link /> can also be done using
    postSelectedHandler = (id) => {
          this.props.history.push({
                      pathname: '/'+id
                  });
                  //this.props.history.push('/'+id) above command and this is the same;
        }
```
