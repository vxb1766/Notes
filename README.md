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
import {Route,Link} from 'react-router-dom'; 

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
                            <li><Link to={{
                                pathname: '/new-post',
                                hash: '#submit',
                                search: '?quick-submit=true'
                            }}>New Post</Link></li>
                            

                        </ul>
                    </nav>
                </header>
                <div>
                  <Post {...this.props} /> -------(a)
                </div>
                <Route path="/" exact component={Posts}/>
                <Route path="/new-post" component={NewPost}/>
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
```
